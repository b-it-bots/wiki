---
title: "Messages, services and actions"
layout: single
tags:
  - ROS
categories:
  - conventions
classes: wide
---

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
Depending on the repository you are working on, the meta-package is related to the domaing, e.g. `mdr_planning_msgs` or `mdr_navigation_actions`
