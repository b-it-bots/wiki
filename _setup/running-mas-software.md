---
title: Running the MAS software
classes: wide
toc: true
---
If you are an @home member, you can setup your [development environment](https://github.com/b-it-bots/dev-env) by using the scripts as described in the `dev-env` README.

## Setting up a catkin workspace

After following the instructions for [installing the requirements](/setup/installing-requirements), you should create a catkin workspace. By convention, we recommend naming your workspace `kinetic`

```
mkdir -p ~/kinetic/src && cd ~/kinetic
```

Next we'll use [wstool](http://wiki.ros.org/wstool) to specify which b-it-bots repositories should be cloned your workspace. In the case of @home, for example:

```
wstool init src
wstool merge -t src https://raw.githubusercontent.com/b-it-bots/mas_domestic_robotics/kinetic/mas-domestic.rosinstall
```

## Get the code and dependencies

Using wstool, we clone all the repositories to your workspace:

```
  wstool update -t src
```

Next we use `rosdep` to install all the dependencies required by the packages to your system:

```
  rosdep install --from-paths src --ignore-src --rosdistro=kinetic -y
```


## Building your workspace
You'll first need to install [catkin-tools](https://catkin-tools.readthedocs.io/en/latest/) and finally compile the repository:

```shell
cd ~/kinetic
catkin build
```

In order to be able to run what you just compiled, you should source your catkin workspace:

```shell
source ~/kinetic/devel/setup.bash
```

The last command should be added to the ~/.bashrc file so that they do not need to be executed every time you open a new terminal.
