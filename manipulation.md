## Starting and controlling 7DOF arm on Jenny

In order to work with Jenny you need to be connected in care bot developers network.

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
Perform emergency stop procedure with controller. 



3) In third window (your computer):
```
 roslaunch mdr_bringup dashboard.launch 
```

This command opens the dashboard.

Press "Initialize all"  and "Recovery all" buttons on dashboard.
(If emergency stop  is still red, perform emergency stop procedure again. After doing this,  don't use "Initialize all" button any more - use just "Recovery all" button.

Unselect  "confirm command".

# Recommendation:
- Check if the tray is up 
- Head always back or back table
- Torso front or front extreme

Be careful for the gripper!  To go from "Spherical open" to any other position always go to "Cylindrical open" and then other positions, because fingers may collide!
Avoid collisions such as: from "cyl_closed"   to "spher_open" and vice versa - DANGEROUS!!!

4) other window pc1 roslaunch mdr_lwr lwr.launch (arm controller-launching arm and realicing brakes) (when you hear a click means its unlocked)


5) other window (your computer) export ROS_MASTER_URI=http://192.168.1.101:11311 (look for any ros command in pc1 to check connection.....such as rostopic list)
rviz in that console after export

6) other window connect to pc2 and run (arm packages) roslaunch mdr_moveit_cob move_group.launch .....for using movit library

7)other window connect to pc2: rosrun moveit_commander moveit_commander_cmdline.py (to control the arm from the terminal)

Specify what group to use: use arm...all others are in dash board
go home (home position) (to see available settings rosed mdr_moveit_con3-1.srdf)
go look_at_table, etc.
go folded


8)
To turn off: firt move arm folded (go folded)...torso home,   and base in start position......Sudo shutdown now (to turn off jenny) on each cob (1,2,3)

turn the key on jenny to left direction

turn current down 
pull cable off 
shutdown power supply
put down em controller on charging station

