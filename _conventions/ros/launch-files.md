---
title: Launch files
layout: single
tags:
  - ROS
categories:
  - conventions
classes: wide
---

# launch-files

## Skills and Actions

1. All the arguments of the component itself and the included files should be defined using at the top of the file:

   ```markup
    <arg="" default=""/>
   ```

   Then when including the launch file, the arguments defined at the top will be passed like this:

   ```markup
    <include="">
        <arg="" value=""/>
    </include>
   ```

2. Remapping - Convention?

## Scenarios

A scenario lunch file must always contain: 1. The argument with the scenario name as it is written on the package, i.e. `mdr_scenario_name`.  
This argument corresponds to the name of the speech grammar as well. 2. Should include arguments for all three of Jenny's computers.  
1. Will mostly contain `include` tags to other components which have their own launch files

* PC1: Navigation, Planning, Data recording
* PC2: Manyears, Perception, Manipulation
* PC3: Speech
  1. The values of all arguments for all the components launched on the scenario must be specified on this launch file.

