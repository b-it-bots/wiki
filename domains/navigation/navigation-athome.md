## Navigation

###### Bringup the robot
First export the environment to be used:
```bash
export ROBOT_ENV=brsu-C069
```

Launch the robot:
```bash
roslaunch mdr_bringup robot.launch
```
Launch the navigation node
```bash
roslaunch mdr_2dnav 2Dnav.launch
```

##### Create navigation goals and orientations
First you need to create the files where goals will be saved:

```
touch navigigation_goals.yaml
touch orientation_goals.yaml
```
##### Localize the robot
In rviz:
1. Select the 2D pose estimate
2. Click the position near the robot
3. Move with joystick
4. Launch navigation tools (in yb2)
```
roscd mcr_default_env_config
cd brsu-C069
rosrun mcr_navigation_tools save_map_poses_to_file
```

### Teleoperate the robot

#### In simulaltion
```bash
rosrun gazebo_ros gzclient (this should launch automatically)
roslaunch mir_teleop teleop_joypad.launch (this should launch automatically)
```
### Autonomous

#### Teleoperate the robot
```
roslaunch mir_teleop teleop_joypad.launch (this should launch automatically)
```

#### On the real robot
TODO: @home version of this?
Run move_base
```
rosrun mir_move_base_safe move_base_safe_server.py
rosrun mir_move_base_safe move_base_safe_client_test.py [source] [dest]



```
