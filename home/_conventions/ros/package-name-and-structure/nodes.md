---
title: ROS nodes
layout: single
tags:
  - ROS
categories:
  - conventions
classes: wide
---

# Creating a new node

## General Rules

If you implement a ROS node some rules need to be followed: 1. The name of the file containing the ROS node has to be extend by " node". For instance: `whole_body_controller_node.cpp` 2. The node name passed to the `ros::init()` function should never include the repository specific prefix. 3. In the launch file of a node, the namespace tag \(`ns="..."`\) needs to be added. The name of the meta-package in which the concerned package is located in, has to be used as this namespace. For instance:

```markup
<node pkg="mcr arm cartesian control " type="
arm_cartesian_control" name="
mcr_arm_cartesian_control " ns="mcr_manipulation "
output="screen" respawn="false"/>
```

In general, the algorithmic part of a component has to be developed framework independent \(i.e. without any ROS specific artefacts\), e.g. in C++ classes. In case of a framework change it is much easier to port a component with strict separation. The ROS node then only wraps your classes in order to get connected \(by topics, actions, etc.\) to the ROS world.

## Dynamic Parametrization

Many algorithms have parameters \(thresholds, velocities, filenames, etc.\) which need to be configured in order to let the algorithm work properly. ROS provides an easy to use functionality called [dynamic reconfigure](http://wiki.ros.org/dynamic_reconfigure), which allows dynamic parametrization \(through a GUI\) while the component is already running. Therefore it is recommended, if an algorithm/component has configuration parameters, to use this embedded functionality. The GUI can be launched with the following command:

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

See the [template](https://github.com/b-it-bots/wiki/tree/021d5ee127ac33c704fd5bbda1545cbcdf191bdc/_conventions/ros/wiki/templates/templates/README.md#skills) for more information.

## Scenarios

Should be implemented as classes which inherit `smach.StateMachine`. They will ideally contain only skills of the robot and the minimum number of `smach.State`s as possible.

Ideally, the scenarios will be substituted soon with a proper planner.

