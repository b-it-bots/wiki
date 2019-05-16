---
title: ROS packages naming and structure
layout: single
tags:
  - ROS
categories:
  - conventions
classes: wide
---

# package-name-and-structure

In order to create a new ROS package for one of the repositories some rules need to be considered:

1. The package name has always the following format:

   ```text
    prefix_my_package_name
   ```

2. Use the right prefix for every repository: a. `mas_domestic_robotics`: `mdr_` b. `mas_industrial_robotics`: `mir_` c. `mas_common_robotics`: `mcr_`
3. Use lowercase.
4. Separate words in the package name by underscores \( \_ \).

Examples for creating packages according to the above described rules are as follows:

```text
catkin create_pkg mdr_grasp_planning
catkin create_pkg mir_whole_body_control
catkin create_pkg mcr_object_detection
```

## Folder structure

Every ROS package within our repositories has to strictly match the following structure:

```text
.
├── common
│   ├── config
│   ├── include
│   │   └── <package_name>
│   ├── src
│   │   └── <package_name>
│   ├── test
│   └── tools
├── ros
│   ├── config
│   ├── include
│   │   └── <package_name>
│   ├── launch
│   │   |— <package_name>.launch
│   ├── rviz
│   │   |— <package_name>.rviz
│   ├── scripts
│   │   └── <package_name>
│   ├── src
│   │   └── <package_name>_node
│   ├── test
│   └── tools
├── CMakeLists.txt
├── package.xml
├── setup.py
└── README.md
```

In short:

* ROS-independent code goes into the `common` folder
* the `ros` folder contains a ROS-wrapper for the functionality you are adding

### Meta-packages

If the package you are creating is meant to contain other packages inside of it, it needs to have instead the following structure:

```text
./<meta_package_name>
└── <meta_package_name>
    ├── CMakeLists.txt
    ├── package.xml
    └── README.md
```

