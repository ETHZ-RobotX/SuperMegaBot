---
layout: default
title: How to drive the SMB
parent: Operating the SMB
nav_order: 4
---

# How to drive the SMB? 
{: .no-toc}
This documentation explains the basic steps about how to safely use the SMB robot.

Please inform oilter@ethz.ch for any missing or unclear instruction.
{: .smb-mention }

## Table of Contents
* Table of contents
{: .toc}



## Remark
Due to the nature of the development process, some extra bugs, errors, hardware problems or safety critical issues, that are not mentioned here, might arise. If this is the case, please refer to the [FAQ document](FAQ.md) and the issue page. Feel free to add new issue! 

#### [Issue Page](https://github.com/ETHZ-RobotX/SuperMegaBot/issues)


<br/> <br/>
### Emergency Stop
For safety purposes, the power input to the motor controller can be cut off by de-energizing a contactor that is part of the [SMB emergency stop system](https://unlimited.ethz.ch/display/ROBOTX/SMB+Emergency+Stop+System).\
Emergency buttons are in series so if one of them is pushed e-stop is activated! This means, the motor controller and thus motors are not powered anymore, robot stops! 
<p align="center">
  <img style="right;"  src="images/E-Stop.png" width="300" title="Remote Emergency Stop">
</p>



<br/><br/>



### RC Connection and Transmitter
When driving the SMB base using the RC transmitter, there is an additional switch on the RC Transmitter to stop all motor movement. It is located on the lower back left of the RC Transmitter with the name [Emergency Stop Switch](images/RCTransmitter.png) and can be used to activate the safety stop functionality of the motor controller powering the motors. The safety stop is activated in the lower position (0).\
Note that when the software overrides the RC commands. 

## Steps

In the document there are two terminal types:

1. Terminal of host PC: The terminal that has access to host pc system.
   
2. Terminal of SSH: The terminal that has SSH connection to the SMB, therefore has access to the SMB system.

### Connecting the Battery


Please be sure that you are well informed about the type of the battery you are using. Read the safety document and do not hesitate to ask for help if you are not sure about something!
{: .smb-warning }

While placing the battery into its drawer, visually verify that the wires are not twisted, sheared or wedged into something!
{: .smb-warning }

If you notice or suspect even a small amount of expantion on the battery, inform your supervisor!
{: .smb-warning }

Do not cut the wires!
{: .smb-warning }

Be sure that wire tips are connected to the right way as the color of connected tips should be same! 
{: .smb-warning }

LiPo cells are affected by the same problems as other lithium-ion cells. This means that overcharge, over-discharge, over-temperature, short circuit, crush and nail penetration may all result in a catastrophic failure, including the pouch rupturing, the electrolyte leaking, and fire.
{: .smb-warning }



### Powering Up 

In the SMBs there is an emergency stop system directly connected to the base. Therefore, a wireless e-stop switch is needed to activate the motors. When the [e-stop switch is activated](images/E-Stop.png), motors do not receive any power.\
Keep the wireless e-stop transmitter close by (e.g. attach it to your belt or similar), in order to be able to switch off all power to the motors in case of an unlikely failure of the motor controller resulting in the robot being uncontrollable. Note that the emergency stop is not a brake system so the robot might continue to move due to its inertia.


Please follow the steps carefully.

1. Before doing anything else, be sure that emergency stop buttons are in the activated position so that the motors cannot be powered up.
   * [The Emergency stop button](images/SMB_Backpanel.png) on the back panel is activated.
   * The E-Stop switch is in activated [e-stop switch is activated](images/E-Stop.png).
  
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


You can refer to the [HowToConnectSMB](HowToConnectSMB.md) to learn about how to connect to SMB by using your pc. 
{: .smb-info }

### ShutDown Procedure
SMBs run with ubuntu 20.04, so the general shutdown procedure for an ubuntu computer applies here. For general remarks please see the followings:

Make sure that SMB does not have defined goal position to move to.
{: .smb-warning }

Make sure that SMB has no movement in its motors.
{: .smb-warning }

To shut down the on-board pc 
   ```bash
   # In terminal of SSH to SMB
   sudo poweroff
   ```

