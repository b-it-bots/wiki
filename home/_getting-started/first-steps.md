---
title: Requirements
toc: true
---

# First steps

## Installing the requirements

#### Ubuntu Xenial 16.04 LTS

We recommend you use Ubuntu 16.04 for your development environment. In general, our repository and its related components have been tested using Ubuntu Xenial. Keep in mind that the robots in the lab will also be setup with the latest compatible Ubuntu distribution.

{% hint style="info" %}
If you are not currently using Ubuntu, you can download it to your computer from [http://www.ubuntu.com/download](http://www.ubuntu.com/download)

ROS Kinetic officially supports Ubuntu Wily \(15.10\) and Ubuntu Xenial \(16.04 LTS\). To see other supported platforms please see the [ROS Kinetic installation instructions](http://wiki.ros.org/kinetic/Installation).
{% endhint %}

It is possible to set up a different operating system for your development environment. However is the support for those options very limited or not given at all. In the following you find an approach for Arch-Linux that has been applied by some students, already.

#### Arch-linux

It is possible to setup your development environment by using a Docker-based setup locally. 

### ROS - Robot Operating System

The current supported version of ROS is Kinetic Kame. To install ROS, follow the official installation instructions found here:

{% hint style="info" %}
ROS Kinetic - [http://wiki.ros.org/kinetic/Installation/Ubuntu](http://wiki.ros.org/kinetic/Installation/Ubuntu)
{% endhint %}

Don't forget to initialize `rosdep`:

```bash
sudo rosdep init
rosdep update
```

Finally, a few recommended tools that you can install include [wstool](http://wiki.ros.org/wstool) and [catkin-tools](https://catkin-tools.readthedocs.io/en/latest/):

```text
sudo apt install python-wstool python-catkin-tools 
```

### Git - Version Control

#### Installation

Install the Git core components and some additional GUI's for the version control:

```text
 sudo apt-get install git-core gitg gitk
```

#### Set Up Git

Now it's time to configure your settings. To do this you need to open a new Terminal. First you need to tell git your name, so that it can properly label the commits you make:

```text
 git config --global user.name "Your Name Here"
```

Git also saves your email address into the commits you make.

```text
 git config --global user.email "your-email@youremail.com"
```

#### Add your ssh key to GitHub

It is recommended that you use ssh to connect to GitHub. For more information read our guide to [Create an ssh key](running-mas-software/tips.md#creating-your-ssh-key) or you can read GitHub's documentation on ssh [here](https://help.github.com/articles/connecting-to-github-with-ssh/). 

{% hint style="warning" %}
Make sure that you are following the instructions for Linux.
{% endhint %}

## GitHub setup

Make sure you have joined the b-it-bots organization by visiting [https://github.com/b-it-bots](https://github.com/b-it-bots/mas_domestic_robotics) 

### Fork the b-it-bots@home repositories

Depending on what you are working on, you might want to fork different repositories. For most people working on the following areas, [mas\_domestic\_robotics](https://github.com/b-it-bots/mas_domestic_robotics) will be more than enough, but here are some other repositories you might want to fork:

{% tabs %}
{% tab title="Manipulation" %}
Required:

* [mas\_domestic\_robotics](https://github.com/b-it-bots/mas_domestic_robotics)
{% endtab %}

{% tab title="Speech" %}
Required:

* [mas\_domestic\_robotics](https://github.com/b-it-bots/mas_domestic_robotics)
{% endtab %}

{% tab title="Navigation" %}
Required:

* [mas\_domestic\_robotics](https://github.com/b-it-bots/mas_domestic_robotics)
{% endtab %}

{% tab title="Perception" %}
Required:

* [mas\_domestic\_robotics](https://github.com/b-it-bots/mas_domestic_robotics)
* [mas\_perception](https://github.com/b-it-bots/mas_perception)

Optional:

* [dataset\_interface](https://github.com/b-it-bots/dataset_interface)
{% endtab %}

{% tab title="Planning" %}
Required:

* [mas\_domestic\_robotics](https://github.com/b-it-bots/mas_domestic_robotics)

Optional:

* [mas\_execution\_manager](https://github.com/b-it-bots/mas_execution_manager)
* [mas\_knowledge\_base](https://github.com/b-it-bots/mas_knowledge_base)
* [action-execution](https://github.com/b-it-bots/action-execution)
{% endtab %}

{% tab title="HRI" %}
Required:

* [mas\_domestic\_robotics](https://github.com/b-it-bots/mas_domestic_robotics)

Optional:

* [mas\_hri\_interface](https://github.com/b-it-bots/mas_hri_interface)
{% endtab %}
{% endtabs %}

{% hint style="info" %}
To find out how to fork a repo, [use GitHub's guide](https://help.github.com/articles/fork-a-repo/).
{% endhint %}

