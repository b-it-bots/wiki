## Mapping for simulation


#### Run simulation related nodes
Run roscore
```
roscore
```

Launch the robot (In another terminal)
```
roslaunch mir_bringup_sim robot.launch
```

Run gazebo simulator (In another terminal)
```
rosrun gazebo_ros gzclient
```

Run rviz (In another terminal)
```
rosrun rviz rviz
```
[To setup the RViz, please go to the bottom of this page.]

#### Generate map
Run 2D SLAM (In another terminal)
```
roslaunch mir_2dslam 2dslam.launch
```

Now there should be robot in an empty map in RViz.

Move the robot around the map. (In another terminal)
```
roslaunch mir_teleop teleop_keyboard.launch
```
[WSAD keys set the robot in motion and "Space bar" stops that motion.]
As you move the robot around, you should be able to see walls appearing in the map in RViz and all the other area will be free.
After you have mapped the whole environment, you can save the map in config map directory.

Move to map config directory (In another terminal)
```
roscd mcr_default_env_config
```
Then make a directory and move inside that newly created directory
```
mkdir test_map
cd test_map
```
Now you can save the map that you just created
```
rosrun map_server map_saver
```
This will ideally create 2 files namely `map.pgm` and `map.yml`.
Now you can exit out of `mir_2dslam` execution.
You can also exit from `mir_teleop`, `gazebo`, `mir_bringup_sim` 

#### Making the map usable
In order to use this map in future to navigate, follow the following steps
Add files where the goals will be saved (in the same directory where the map files have been saved)
```
touch navigation_goals.yaml
touch orientation_goals.yaml
```

Make a copy of the existing launch file.
```
cd ~/catkin_ws/src/mas_common_robotics/mcr_environments/mcr_gazebo_worlds/ros/launch
cp brsu-c025-sim.launch test_map.launch
```
Inside `test_map.launch`, edit the argument of "robot_env"(line 10). Replace `brsu-c025-sim` with `test_map`. Save this file.

Make a copy of xacro file.
```
cd ~/catkin_ws/src/mas_common_robotics/mcr_environments/mcr_gazebo_worlds/common/worlds/
cp brsu-c025-sim.urdf.xacro test_map.urdf.xacro
```
Now your newly created map should be ready for use.

## Navigation
Run the commands from "Run simulation related nodes" as mentioned above to bring the robot up.

Launch the navigation node
```
roslaunch mir_2dnav 2Dnav.launch
```

Add `PoseArray` in RViz and change its topic to `/particlecloud`. 
Now you will be able to see red arrows around the robot. These arrow show the pose of the robot. 
You now need to localize the robot to get its correct pose.
Move the robot around the map. (In another terminal)
```
roslaunch mir_teleop teleop_keyboard.launch
```
Rotate the robot in its place using QE keys. You will notice the red arrows converging around the robot.
Once the the robot is reasonably localised, you can navigate the robot around in 2 ways.

#### 1. GUI (RViz)
Click on the `2D Nav Goal` and select a goal on the map.

#### 2. Terminal based (ROS)
Please refer `navigation-atwork.md`


## RViz setup
![alt text](https://github.com/DharminB/wiki/blob/atwork_mapping/guides/domains/navigation/rviz_config.png)

Add `Map`, `RobotModel`, `LaserScan` using the "Add" button in bottom left corner of "Display" section of RViz.

In `Map`, change the topic to `/map`

In `LaserScan`, change the topic to `/scan_front`. Add another `LaserScan` and change its topic to `/scan_rear`.

In global option, change the `Fixed Frame` to `map`.

You can also add another `PoseArray` and change its topic to `/move_base/GlobalPlannerWithOrientation` to visualise the plan created by the `mir_2Dnav` node.

