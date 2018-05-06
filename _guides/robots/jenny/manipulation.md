---
title: "Manipulation using the 7DOF Kuka Lighweight Arm"
tags:
  - Care-O-Bot
---

## Starting and controlling 7DOF arm on Jenny

In order to work with Jenny you need to be connected in "care-o-bot-developers" network.

Jenny has 3 PCs:

```
PC1: Navigation and sensors, arm controller

PC2: Arm packages and perception

PC3: Speech recognition

```
# Procedure:

1) In first window:

```
ssh username@cob3-1-pc1
roscore
```

2)  In second window also connect to PC1 (use cob1 alias):
```
roslaunch mdr_bringup robot.launch
```
Perform emergency stop procedure with controller before continuing.


3) In third window (your computer):
```
 roslaunch mdr_bringup dashboard.launch
```

This command opens the dashboard.

Press "Initialize all"  and "Recovery all" buttons on dashboard. (If emergency stop  is still red, perform emergency stop procedure again. After doing this,  don't use "Initialize all" button any more -  just use "Recovery all" button from now on)

Unselect  "confirm command" to make controlling simple.


4) In additional window also connect to PC1:

```
  roslaunch mdr_lwr lwr.launch
```

Starting arm controller - launching arm and releasing the brakes (when you hear a click means its unlocked).


5) Another window (your computer):

```
 export ROS_MASTER_URI=http://192.168.1.101:11311
```

Look for any  ROS command in PC1 to check connection, e.g.

```
rostopic list
```

If the connection is working you can use RVIZ:

```
rviz
```

If the OMPL library is not recognized in RVIZ:

```
export $ROS_IP=ip_adress_of_your_com
```

Restart RVIZ


6) In another window connect to PC2 and run arm packages for using "MoveIt" library:

```
roslaunch mdr_moveit_cob move_group.launch
```

7) In one more window connect to PC2. Run command for moving the arm from the terminal:

```
rosrun moveit_commander moveit_commander_cmdline.py
use arm
```

Some of the example commands for positioning arm are :

```
go home
go look_at_table
go folded
```

To see more available settings:
```
rosed mdr_moveit_con3-1.srdf
```

8)
To turn off everything:
- First move arm to folded position (go folded)
- Move torso to home position  
- Move base in start position.

To turn off Jenny on each cob (1, 2, 3):

```
sudo shutdown now
```

# In case of emergency stop activated:  
There are three versions to recover LWR - Arm running again after an emergency stop and you need to be connected on new pc1 terminal (it is not possible to recover the arm with dash board):

Version a) Call the recover service of the arm by running the command:
```
rosservice call /arm_controller/lwr_node/recover
```
If you hear that the arm clicks and that means that it is already active. This is to not restart the arm controller.


Version b)
Sometimes the ROS node which communicates with the LWR loses connection to the controller. In this case restart the node:
```
roslaunch mdr_lwr lwr.launch
```
Version c)
In some cases it is not possible to recover the LWR properly after an emergency stop has been issued. In such a situation the LWR controller must be rebooted and reinitialized. To reboot the controller, login to the lbr-box via telnet with following command:
```
telnet lbr-box
```
and reboot using the following the command:
```
reboot
```
Wait until the controller is up and running again.  Then perform the initialization procedure:
```
ssh username@cob3-1-pc1
telnet lbr-box
<l
```
Wait for the line “Stable state RUNNING reached!”. If you do not see this line, contact your robot administrator.

# Recommendation:
- Check if the tray is up
- Head always back or back table
- Torso front or front extreme


Be careful with the gripper!  To go from "Spherical open" to any other position always go first to "Cylindrical open" and then other positions, because fingers may collide!

Going from "cyl_closed"   to "spher_open" and vice versa - DANGEROUS!!!
