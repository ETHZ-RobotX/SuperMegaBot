# How to Use SMB? 
> This documentation explains the basic steps about how to use SMB robot. The documentation might lack of of some information since the updated SMB software is still work in progress!  
> Please inform oilter@ethz.ch for any missing or unclear instruction.

## Table of Contents
- [How to Use SMB?](#how-to-use-smb)
  - [Table of Contents](#table-of-contents)
  - [Remark](#remark)
      - [Issue Page](#issue-page)
    - [Emergency Stop](#emergency-stop)
    - [RC Connection and Controller](#rc-connection-and-controller)
  - [Steps](#steps)
    - [Connecting the Battery](#connecting-the-battery)
    - [Powering Up](#powering-up)
    - [Connecting to SMB](#connecting-to-smb)
    - [Running the Software](#running-the-software)
    - [ShutDown Procedure](#shutdown-procedure)



## Remark
Due to the nature of the development process, some extra bugs, errors, hardware problems or safety critical issues, that are not mentioned here, might arise. If this is the case, please refer to the [FAQ document](FAQ.md) and the issue page. Feel free to add new issue! 

#### [Issue Page](https://github.com/ETHZ-RobotX/SuperMegaBot/issues)


<br/><br/>
### Emergency Stop
For safety purposes, the power input to the motor controller can be cut off by de-energizing a contactor that is part of the [SMB emergency stop system](https://unlimited.ethz.ch/display/ROBOTX/SMB+Emergency+Stop+System).\
Emergency buttons are in series so if one of them is pushed e-stop is activated! This means, the motor controller and thus motors are not powered anymore, robot stops! 
<p align="center">
  <img style="right;"  src="images/E-Stop.png" width="300" title="asd">
</p>



<br/><br/>



### RC Connection and Controller
When driving the SMB base using the RC transmitter, there is an additional switch on the RC Transmitter to stop all motor movement. It is located on the lower back left of the RC Transmitter with the name [Emergency Stop Switch](images/RCTransmitter.png) and can be used to activate the safety stop functionality of the motor controller powering the motors. The safety stop is activated in the lower position (0).\
Note that when the software overrides the RC commands. 

## Steps

In the document there are two terminal types:
1) Terminal of host PC: The terminal that has access to host pc system.
2) Terminal of SSH: The terminal that has SSH connection to the SMB, therefore has access to the SMB system.

### Connecting the Battery

!!!![TODO]!!!!

Prepare such a document for summer school area! 

https://ethz.ch/content/dam/ethz/special-interest/mavt/department-dam/departement/documents/Code%20of%20Conduct%20Rechargeable%20Batteries.pdf


!!!![TODO]!!!!

:exclamation: Please be sure that you are well informed about the type of the battery you are using. Read the safety document and do not hesitate to ask for help if you are not sure about something. 

:exclamation: While placing the battery into its drawer, visually verify that the wires are not twisted, sheared or wedged into something. 

:exclamation: If you notice even a small amount of expantion on the battery, inform your supervisor!

:exclamation: Do not cut the wires! 

:exclamation: Be sure that wire tips are connected to the right way as the color of connected tips should be same! 

:exclamation: LiPo cells are affected by the same problems as other lithium-ion cells. This means that overcharge, over-discharge, over-temperature, short circuit, crush and nail penetration may all result in a catastrophic failure, including the pouch rupturing, the electrolyte leaking, and fire.




### Powering Up 

In the SMBs there is an emergency stop system directly connected to the base. Therefore, a wireless e-stop switch is needed to activate the motors. When the [e-stop switch is activated](images/EB_Activated.jpg), motors do not receive any power.\
Keep the wireless e-stop transmitter close by (e.g. attach it to your belt or similar), in order to be able to switch off all power to the motors in case of an unlikely failure of the motor controller resulting in the robot being uncontrollable. Note that the emergency stop is not a brake system so the robot might continue to move due to its inertia.


Please follow the steps carefully.

1. Before doing anything else, be sure that emergency stop buttons are in the activated position so that the motors cannot be powered up.
   * [The Emergency stop button](images/SMB_Backpanel.png) on the back panel is activated.
   * The E-Stop switch is in activated [e-stop switch is activated](images/EB_Activated.jpg).
  
2. Turn on the RC transmitter.
   * Be sure that the transmitter is connected to the right smb: check the number on the screen of the transmitter and the number that is written back panel of the smb 
   * Be sure that the [Emergency Stop Switch of the RC Transmitter](images/RCTransmitter.png)  is in the position of 0. It gives '0' commands to the motots . 
   * BUT IF THERE IS A PROBLEM WITH THE CONTROLLER (e.g. the robot is uncontrollable) USE THE EMERGENCY STOP SWITCH! THAT SAFETY STOP SWITCH MIGHT NOT WORK 

3. Power up the base using the switch [Base Power Switch](images/SMB_Backpanel.png) . This switch activates also the wireless e-stop receiver.
   * Since the wireless e-stop system is energized and it is in the activate state (we did it so at step 1), we can deactivate the [Emergency Stop Button on the SMB](images/SMB_Backpanel.png). 
  
4. Deactivate the wireless e-stop by pulling out the button.  
    * As soon as the emergency stop circuit is closed, you should hear a mechanical clicking sound. This clicking sound originates from the contactor that physically closed the power circuit to the motors. Also, the LED on the wireless e-stop transmitter should be blinking at a regular interval. 
    * Now you are able to drive drive the smb via RC
  
 1. Be sure that the safety stop switch on the RC transmitter is functional by doing a small test.
    * Try to drive the robot while it is in the position 0 -> no movement 
    * Flipping the safety stop switch on the RC remote to position 1 should allow movement of the robot. Use the right control stick on the RC transmitter to steer the SMB. 
    * Switching the safety stop on the Remote back into position 0 should stop the robot. Try again to to control the robot while switch is in position 0. It should not move. 
5. Bring the safety stop switch to the position 1 again. Small movements on the stick are already enough to command forward motion. 

### Connecting to SMB 

In order to power-up the computer on the SMB use the [Payload Power Switch](Images/SMB_Backpanel.png) Close the lid of the switch to prevent shut-down by mistake.
In order to connect to SMB remotely, the host PC should connect the Wifi of the SMB: 
  * Wifi (SSID): smb-<SMB_ROBOT_NUMBER>
  * Password: SMB_<SMB_ROBOT_NUMBER>_RSS or *_RSL

Once you are connected, from the terminal you should connect the SMB via SSH. **The ip addresses of every SMB is 11.0.0.5** .

> Note that there might be an error in the host PC while trying to connect the SMB via ssh. Please read the terminal and use the suggested command in terminal to remove the previous ssh connection settings. 

```bash
# In the terminal of host pc
ssh smb@11.0.0.5
# Password: smb

#! Terminal becomes terminal of SSH! 

# To connect the SMB to Internet 
nmcli connection up
```
Once you are connected to the SMB you will see an IP address and port tuple on the terminal starting with 'http://'. Please save it since we will need it in the next step. 

If you do not see such a tupple, please start the roscore and check the part ROS_MASTER_URI.

```bash
# In the terminal of SSH
roscore
# See the part of ROS_MASTER_URI
```





### Running the Software 

In order to use the visualization tools of ROS, we will set the SMB as ROS master on our local machine:

```bash
# In the terminal of host pc
export ROS_MASTER_URI=http://11.0.0.5:<port>
# the ip and port tuple we have saved in the previous step  
```

Now we can run SMB software and visualize it in the host pc. 

In order to give commands from the host pc to SMB, ROS_IP should be set. 

```bash
# In the terminal of host pc

ifconfig
# See the ip addres of wlp4s0
# It is probably 11.0.0.100

export ROS_IP=<wlp4s0_ip>
# the ip and port tuple we have saved in the previous step  
```

> Note that at every new terminal you have to repeat the steps under the title of Running the Software. Please refer to [the NotionsAndDevices document](NotionsAndDevices.md) for more information related to 'export' command.

To use the packages and run the software please refer to the [HowToRunSoftware](HowToRunSoftware.md)


### ShutDown Procedure
SMBs run with ubuntu 20.04, so the general shutdown procedure for an ubuntu computer applies here. For general remarks please see the followings:
* Make sure that SMB does not have defined goal position to move to. 
* Make sure that SMB has no movement in its motors.
* To shut down the on-board pc 
   ```bash
   # In terminal of SSH to SMB
   sudo poweroff
   ```

