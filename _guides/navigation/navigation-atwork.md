---
title: Mapping @Work
tags:
  - navigation
---

Note : For simulation please check [simulation_mapping.md](/guides/domains/navigation/simulation_mapping.md)


Export the youbot ssh alias

```
export_yb2
```

To shh the youbot (in all terminals):

```
yb2
```

this is the alias to connect to the youbot

Run roscore

```
roscore
```

Launch the robot

```
roslaunch mir_bringup robot.launch
```
Run rviz

```
rosrun rviz rviz
```
Set the global frame to `base_link`

##### Launch SLAM

```
roslaunch mir_2dslam 2dslam.launch
```

Note: the map is built using the front laser's only

##### Run the map saver
Go to the folder with the map
`roscd mcr_default_env_config`

By using `ls` you can see several folders corresponding to existing environments. You can either use an existing map or create a new one:

```
mkdir [map_name]
```

Before running the map_saver you need to be located in the environment folder:
```
cd [map_name]
```

And then run:
```
rosrun map_server map_saver
```

This will create two files: a `map.pgm` and `map.yml`.

Finally, to use the map that you just created you need to check which map will be loaded by the navigation stack:
```
echo $ROBOT_ENV
```

If you need to change it:
```
export ROBOT_ENV=[map_name]
```

Note: Usually the `.rosc` script is used to set the environment, among other variables.

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
touch navigation_goals.yaml
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
rosrun mir_move_base_safe move_base_safe_client_test.py [source] [dest]
```

##### Navigation test
```
roslaunch mir_basic_navigation_test refbox_parser.py
```
