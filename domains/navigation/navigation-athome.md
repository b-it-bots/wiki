## Navigation
###### Bringup the robot
First export the environment to be used:
```export ROBOT_ENV=brsu-C025```

Launch the robot:
```
roslaunch mir_bringup robot.launch
```
Launch the navigation node
```
roslaunch mir_2dnav 2Dnav.launch
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
cd brsu-C025
rosrun mcr_navigation_tools save_map_poses_to_file
```
Run move_base
```
rosrun mir_move_base_safe move_base_safe_server.py
rosrun mir_move_base_safe move_base_safe_client_test.py [source] [dest]```

##### Navigation test
```
roslaunch mir_basic_navigation_test refbox_parser.py
```
