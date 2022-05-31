# Model Predictive Control Tutorial

## Goal
Use MPC to drive the MPC to an arbitrary pose

## 0.0 Recap - Differential Dynamic Programming

Figure on SLQ / ILRQ algorithm goes here:



ILQR-MPC produces affine control policies. With the policy, you can 

### Basic steps algorithm:
Take current control policy [K, u*] to compute control inputs:  u= K(t)*x(t) + u*(t)
Forward integrate current state x_0 with the current policy to get  state and input trajectories over time horizon
Compute second order approximation of the cost functions arround state and input trajectories
Solve the Riccati Equation to get a new affine control policy
Use a line search to find the best interpolation between the current and the new policy




M. Neunert et al., “Fast nonlinear Model Predictive Control for unified trajectory optimization and tracking,” in 2016 IEEE International Conference on Robotics and Automation (ICRA), May 2016, pp. 1398–1404. doi: 10.1109/ICRA.2016.7487274.


## 0.1 Automatic Differentiation

In our MPC framework we often use automatic differentiation to compute derivatives of system flow maps and cost functions.
We use CppAD Codgen as the implementation.
### Implications:
- You cannot use `std::cout` within the auto generation methods
- All computations need to be done with the `ad_scalar_t` type instead of `double`.
  `double` can be converted to `ad_scalar_t` implicitly.
  For “Eigen” matrices and vectors, you need to use the `.cast<ad_scalar_t>()` method to convert explicitly.



## 1. System Modeling
Add a picture of SMB on a slope. Visualize body frame, world frame. Add arrows for $v_x$ and $omega_z$ 


Derive flow map $\boldsymbol{\dot{x}} = f(\boldsymbol{x},\boldsymbol{u},t)$ for mobile robot:

#### Given:

State $\boldsymbol{x}$:
- $(x,y,z)$ position in world frame
- $(q_x, q_y, q_z, q_w)$ quaternion rotation body to world frame

Time $t$

Control input $\boldsymbol{u}$:
- $v_x$: linear velocity in body frame (motion relative to world frame)
- $\omega_z$ : angular velocity in body frame (motion relative to world frame)

#### Wanted:
$\frac{\delta}{\delta t}(x,y,z, q_x, q_y, q_z, q_w, t)^T$

Hints:



Implement system model in `smb_common/smb_mpc/src/SmbSystemDynamics.cpp`

## 2. Cost function

Implement a cost function that penalizes deviations from the point $(x,y,\theta)$: $(2m, 5m, 90deg)$

Method: `costVectorFunction`
`smb_common/smb_mpc/src/cost/SmbCost.cpp`

Hint:
`costVectorFunction` should return a 3-dim vector (`result`) with three elements. The scalar value of the cost function is `vector^T \cdot vector`

## 3. Reference Tracking

We want to track arbitrary trajectories with the robot.
When selecting a goal in  rviz with the 2D Nav Goal marker,  getParameters receives a trajectory of poses and timestamps.
The method should return a target pose for the time $t$.

Hint: `getParameters` works on double types. No `ad_scalar_t`  type needed here.

The method `costVectorFunction` receives this target pose at the current time $t$. Modify the cost function to track this trajectory.

## 4. Gains

The weight matrices: `QPosition_`, `QPosition_`, `R_` are available in the cost function and are loaded from the configuration file:
`smb_common/smb_mpc/config/task.info`

Find a good set of gains for the robot to track the reference path

## 5. Dynamic System model (optional)

The kinematic system model assumes that the robot velocity can be changed instantaneously. Since this is not possible on physical systems there are going to be tracking errors.

A system model that takes accelerations as inputs and has the base velocity as part of the system state is more realistic since it does not allow for jumps in the velocity profiles.

Checkout the branch `mpc_tutorial/dynamic_model`

Implement a dynamic system model and a costfunction for tracking trajectories.
`smb_common/smb_mpc/src/SmbSystemDynamics.cpp`
`smb_common/smb_mpc/src/cost/SmbCost.cpp`

