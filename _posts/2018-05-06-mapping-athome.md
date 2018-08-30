---
title: Mapping @Home
tags:
  - navigation
  - Care-O-Bot
---

Note: When using Jenny, mapping is run on `cob1`

### Bringup the robot

2. Run roscore:

  ```bash
  roscore
  ```
4. Run rviz:
  ```bash
  rosrun rviz rviz
  ```
  Set the global frame to `base_link`.

#### In simulation

1. Launch the robot:
  ```
  roslaunch mdr_bringup_sim robot.launch
  ```

#### Using the real robot
1. Make sure you have initialized Jenny (see [here](working-on-jenny) for more details).
1. Export Jenny's ssh alias:

  ```
  export_cob1
  ```
  To shh the Jenny (PC1) run the following in all terminals:
  ```
  cob1
  ```
3. Launch the robot:
  ```
  roslaunch mdr_bringup robot.launch
  ```


#### Launch SLAM
##### Building the map
1. Launch the SLAM node:
  ```
  roslaunch mdr_2dslam 2dslam.launch```

  Note: the map is built using the front laser's only.
2. Set the global frame in Rviz to map

3. Move the robot around either by using the joystick or by teleoperation.  

##### To save the map
Maps are stored in `~/catkin_ws/src/mas_common_robotics/mcr_environments/mcr_default_env_config`. An environment, such as `brsu-C025` or `brsu-C069`, is a folder in this directory. Within this folder, the maps, goals and parameters are stored.  

  1. To go to the folder where we will save the map you can run:  
  ```
  roscd mcr_default_env_config
  ```

  By using `ls` you can see several folders corresponding to existing environments.


  2. Before running the `map_saver`, you need to be located in the environment folder. You can either overwrite an existing map by using `cd` or you can create a new one:

  ```bash
  mkdir [map_name] && cd [map_name]
  ```
  For example:
  ```
  mkdir new_map && cd new_map
  ```

  3. Finally, to save the map, just run:  
  ```
  rosrun map_server map_saver```

  This will create two files: a `map.pgm` and `map.yml`.

Finally, to use the map that you just created you need to check which map will be loaded by the navigation stack:  
  ```bash
  echo $ROBOT_ENV
  ```
If you need to change it:  
  ```bash
  export ROBOT_ENV=[map_name]
  ```

Note: Usually the `.rosc` script is used to set the environment, among other variables.
