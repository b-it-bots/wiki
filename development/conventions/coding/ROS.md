# ROS packages

In order to create a new ROS package for one of the repositories some rules need
to be considered:

1. The package name has always the following format:
```
prefix_my_package_name
```
2. Use the right prefix for every repository:  
    a. `mas_domestic_robotics`: `mdr_`  
    b. `mas_industrial_robotics`: `mir_`  
    c. `mas_common_robotics`: `mcr_`  
3. Use lowercase.
4. Separate words in the package name by underscores ( _ ).

Examples for creating packages according to the above described rules are as
follows:
```
catkin create_pkg mdr_grasp_planning
catkin create_pkg mir_whole_body_control
catkin create_pkg mcr_object_detection
```

## Folder structure
Every ROS package within our repositories has to strictly match the following
structure:
```
.
├── common
│   ├── config
│   ├── include
│   │   └── <package_name>
│   ├── src
│   │   └── <package_name>
│   ├── test
│   └── tools
├── ros
│   ├── config
│   ├── include
│   │   └── <package_name>
│   ├── scripts
│   │   └── <package_name>
│   ├── src
│   │   └── <package_name>_ros
│   ├── test
│   └── tools
├── CMakeLists.txt
└── package.xml
```


# ROS Nodes
## General Rules
If you implement a ROS node some rules need to be followed:
1. The name of the file containing the ROS node has to be extend by " node".
For instance:
`whole_body_controller_node.cpp`
2. The node name passed to the `ros::init()` function should never include the
repository specific prefix.
3. In the launch file of a node, the namespace tag (`ns="..."`) needs to be added.
The name of the meta-package in which the concerned package is located
in, has to be used as this namespace. For instance:
```xml
<node pkg="mcr arm cartesian control " type="
arm_cartesian_control" name="
mcr_arm_cartesian_control " ns="mcr_manipulation "
output="screen" respawn="false"/>
```
In general, the algorithmic part of a component has to be developed framework
independent (i.e. without any ROS specific artefacts), e.g. in C++ classes. In
case of a framework change it is much easier to port a component with strict
separation.
The ROS node then only wraps your classes in order to get connected (by topics,
actions, etc.) to the ROS world.

## Dynamic Parametrization
Many algorithms have parameters (thresholds, velocities, filenames, etc.) which
need to be configured in order to let the algorithm work properly. ROS provides
an easy to use functionality called [dynamic reconfigure](http://wiki.ros.org/dynamic_reconfigure), which allows dynamic
parametrization (through a GUI) while the component is already running. Therefore it is recommended, if an algorithm/component has configuration parameters,
to use this embedded functionality. The GUI can be launched with the following
command:
```bash
rosrun rqt_reconfigure rqt_reconfigure
```


# See Also
* [Spaces and Tabs]()
