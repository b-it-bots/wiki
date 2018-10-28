---
title: "Linting"
layout: single
tags:
  - ROS
categories:
  - conventions
classes: wide
---


## Running `roslint` with catkin
Before merging into the main repository `roslint` is ran on all merge requests. Unless all errors are resolved the merge request will be rejected. To test if your changes would pass the `roslint` test locally:
- Add the following lines to your `CMakelists.txt`:

```CMake
find_package(catkin REQUIRED COMPONENTS roslint ...)

roslint_python()  # pep8 linting
roslint_cpp()     # ROS wrapper of Google's cpplint
```


Your `package.xml` should include `roslint` as a build dependency:

```xml
<build_depend>roslint</build_depend>
```

- Build target `roslint`:
  - with `catkin_make`: `catkin_make roslint_<package_name>`
  - with `catkin_tools`: `catkin build --no-deps <package_name> --make-args roslint_<package_name>`
- If build fail copy and execute the gray line that looks something like the following to see more detailed errors:

```
cd <package_source_directory>; catkin build --get-env <package_name> | catkin env -si  /usr/bin/make roslint --jobserver-fds=6,7 -j; cd -
```
![2017-05-06-205659_900x152_scrot](2017-05-06-205659_900x152_scrot.png)


## Running `catkin_lint`

You should also make sure that the `catkin_lint` tests pass; running it from the root of your catkin workspace you can run:

```
catkin_lint --strict --ignore CRITICAL_VAR_APPEND,LINK_DIRECTORY src/mas_domestic_robotics
```

## See Also
* [roslint](http://wiki.ros.org/roslint)
* [catkin_lint](http://fkie.github.io/catkin_lint/)

Proposed linters:
- [C++](http://clang.llvm.org/extra/clang-tidy/)
- [Python](https://pypi.python.org/pypi/pep8)
- [ROS](http://wiki.ros.org/roslint)
