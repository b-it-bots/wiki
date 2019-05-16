---
title: Requirements
toc: true
---

# installing-requirements

## Install Ubuntu

The repository and its related components have been tested under the following Ubuntu distributions:

* ROS Kinetic: Ubuntu 16.04

If you do not have a Ubuntu distribution on your computer you can download it here

[http://www.ubuntu.com/download](http://www.ubuntu.com/download)

## Git - Version Control

### Install Git Software

Install the Git core components and some additional GUI's for the version control:

```text
 sudo apt-get install git-core gitg gitk
```

### Set Up Git

Now it's time to configure your settings. To do this you need to open a new Terminal. First you need to tell git your name, so that it can properly label the commits you make:

```text
 git config --global user.name "Your Name Here"
```

Git also saves your email address into the commits you make.

```text
 git config --global user.email "your-email@youremail.com"
```

### Add your ssh key to GitHub

You can follow GitHub's documentation on ssh [here](https://help.github.com/articles/connecting-to-github-with-ssh/). Make sure that you are following the instructions for Linux.

## ROS - Robot Operating System

### Install ROS

The repository has been tested successfully with the following ROS distributions. Use the link behind a ROS distribution to get to the particular ROS installation instructions.

* ROS Kinetic - [http://wiki.ros.org/kinetic/Installation/Ubuntu](http://wiki.ros.org/kinetic/Installation/Ubuntu)

NOTE: Do not forget to update your .bashrc!

