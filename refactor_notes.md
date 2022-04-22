# Refactor notes

## TODOs

- [ ] refactor smb_common
- [ ] try not include `flir_camera_driver`, currently it will report issue when rosdep install

    ```shell
    ERROR: the following rosdeps failed to install
    apt: command [sudo -H apt-get install -y ros-noetic-flir-camera-driver] failed
    apt: Failed to detect successful installation of [ros-noetic-flir-camera-driver]
    ```

- [ ] suppress unnecessary `rosdep` warnings

    ```shell
    ERROR: the following packages/stacks could not have their rosdep keys resolved
    to system dependencies:
    smb_msf: Cannot locate rosdep definition for [msf_updates]
    spinnaker_camera_driver: Cannot locate rosdep definition for [opencv3]
    smb_sensors: Cannot locate rosdep definition for [versavis]
    smb_navigation: Cannot locate rosdep definition for [traversability_estimation]
    smb_mpc: Cannot locate rosdep definition for [ocs2_comm_interfaces]
    smb_lowlevel_controller: Cannot locate rosdep definition for [message_logger]
    ocs2_frank_wolfe: Cannot locate rosdep definition for [libglpk-dev]
    ocs2_doc: Cannot locate rosdep definition for [doxygen-latex]
    icp_localization: Cannot locate rosdep definition for [ros-noetic-tf2-geometry]
    Continuing to install resolvable dependencies...
    # All required rosdeps installed successfully
    ```

## Other issues

- check the use of packages this year
  - smb_msf
  - compslam
  - cartographer, cartographer_ros, abseil
  - traversability_estimation: [related component has not been fully tested yet!](https://github.com/VIS4ROB-lab/smb_path_planner/wiki/Running-in-simulation#running-with-traversability-estimation) for smb_navigation
- [object_detection](https://github.com/ETHZ-RobotX/smb_object_detection) is currently private (integrate in smb.repos afterwards)

  ```yaml
  object_detection:
    type: git
    url: https://github.com/ETHZ-RobotX/smb_object_detection.git
    version: main
  ```

## Logs

- 220422
  - refactor the whole structure as follows

    ```shell
    ❯ tree -L 2
    .
    ├── core
    │   ├── jenkins-pipeline
    │   ├── odometry_conversion
    │   ├── README.md
    │   ├── record_sensors.sh
    │   ├── smb
    │   ├── smb_control
    │   ├── smb_description
    │   ├── smb_gazebo
    │   ├── smb_lowlevel_controller
    │   ├── smb_mpc
    │   ├── smb_msf
    │   ├── smb_opc
    │   ├── smb_sensors
    │   └── smb_slam
    ├── hardware
    │   ├── flir_camera_driver
    │   ├── robosense_simulator
    │   └── smb_powerstatus
    ├── lib
    │   ├── libnabo
    │   ├── libpointmatcher
    │   ├── ocs2
    │   └── pointmatcher_ros
    ├── misc
    │   ├── catkin_simple
    │   └── cmake_clang_tools
    ├── planning
    │   ├── follow_waypoints
    │   ├── smb_mission_planner
    │   ├── smb_path_planner
    │   └── teb_local_planner
    ├── slam
    │   ├── compslam
    │   └── icp_localization
    └── ui
        ├── multimaster_fkie
        └── smb_rviz_plugins
    ```

  - rename `smb_common` as `core/`
  - fix rosdep install issue
    - add catkin_simple: <https://github.com/catkin/catkin_simple.git>
    - add flir_camera_driver: <https://github.com/ethz-asl/flir_camera_driver.git>
  - add packages
    - planning/follow_waypoints
    - planning/smb_mission_planner
    - ui/multimaster_fkie
