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
│   ├── launch
│   │   |— <package_name>.launch
│   ├── rviz
│   │   |— <package_name>.rviz
│   ├── scripts
│   │   └── <package_name>
│   ├── src
│   │   └── <package_name>_node
│   ├── test
│   └── tools
├── CMakeLists.txt
├── package.xml
└── README.md
```

### Messages, services and actions
If your package defines its own messages, services or actions you should add them to the corresponding meta-package:
```
./<package_name>_msgs
├── action
│   ├── MyAction.action
├── msg
│   ├── MyMessage.msg
├── srv
│   └── MyService.srv
├── CMakeLists.txt
├── package.xml
└── README.md

```

### Meta-packages
```
./<meta_package_name>
└── <meta_package_name>
    ├── CMakeLists.txt
    ├── package.xml
    └── README.md
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

## Skills and actions
Components in our repository should be developed using smach state machines with an actionlib wrapper. This way we can guarantee that they are ready for the planner to use them.

Actions must always:
* have a timeout with a default value
* provide feedback during the execution
* the outcome states should include:
    * REJECTED
    * RECALLED
    * PREEMTED
    * ABORTED
    * SUCCEEDED

See the  [template](wiki/templates/templates#skills) for more information.

## Scenarios
Should be implemented as classes which inherit `smach.StateMachine`. They will ideally contain only skills of the robot and the minimum number of `smach.State`s as possible.

Ideally, the scenarios will be substituted soon with a proper planner.


## Launch Files
### Skills and Actions
1. All the arguments of the component itself and the included files should be defined using at the top of the file:
```xml
<arg="" default=""/>
```

    Then when including the launch file, the arguments defined at the top will be passed like this:
```xml
<include="">
    <arg="" value=""/>
</include>
```
2. Remapping - Convention?

### Scenarios
A scenario lunch file must always contain:
1. The argument with the scenario name as it is written on the package, i.e. `mdr_scenario_name`.  
This argument corresponds to the name of the speech grammar as well.
2. Should include arguments for all three of Jenny's computers.  
NOTE: Does this make sense? Should component launch files handle this instead? Do they have to be arguments?
1. Will mostly contain `include` tags to other components which have their own launch files
    * PC1: Navigation, Planning, Data recording
    * PC2: Manyears, Perception, Manipulation
    * PC3: Speech
3. The values of all arguments for all the components launched on the scenario must be specified on this launch file.

## READMEs
### Package
#### Scenario
#### Actions and Skills
### Meta-packages
### Messages, Services and Action Files

# See Also
* [Spaces and Tabs]()
* [Templates](wiki/templates/templates)
