---
title: "Aliases"
---

In order to be able to run code more smoothly, please use the aliases listed in this README. For your convinience, you can also clone the repository and use the following instructions:

## Using the b-it-bots aliases and scripts
The repository b-it-bots/dotfiles contains a folder with some useful aliases and scripts for your `.bashrc`. To use them, first clone this repository to your home:
```bash
cd ~/
git clone gitgate@mas.b-it-center.de:b-it-bots/dotfiles.git
```
After you have cloned the repository, update the *`username`* with your username in the PCs.

Finally, simply add this lines to your `.bashrc` file:

```bash
source ~/dotfiles/alias/common.sh
source ~/dotfiles/alias/athome_aliases
source ~/dotfiles/alias/atwork_aliases
```


## General
```
alias export_rosip='export ROS_IP=$(hostname -I)'
```

## @home
### Jenny

#### ssh
```
alias cob1='ssh -X username@cob3-1-pc1'
alias cob2='ssh -X username@cob3-1-pc2'
alias cob3='ssh -X username@cob3-1-pc3'
```

#### ROS
```
alias export_cob='export ROS_MASTER_URI=http://cob3-1-pc1:11311/'
```
##### PC1
```
alias bringup='roslaunch mdr_bringup robot.launch'
alias arm_bringup='roslaunch mdr_lwr lwr.launch'
alias recover_arm='rosservice call /arm_controller/lwr_node/recover'
```
##### PC2
```
alias moveit='roslaunch mdr_moveit_cob move_group.launch'
alias camera_bringup='roslaunch cob_bringup openni2.launch camera:=cam3d'
```

## @work
### youBot

#### ssh
```
alias yb1='ssh -X username@youbot-brsu-1-pc1'
alias yb2='ssh -X username@youbot-brsu-2-pc1'
alias yb3='ssh -X username@youbot-brsu-3-pc1'
alias yb4='ssh -X username@youbot-brsu-4-pc1'
```


### ROS
```
alias export_yb1='export ROS_MASTER_URI=http://youbot-brsu-1-pc1:11311/'
alias export_yb2='export ROS_MASTER_URI=http://youbot-brsu-2-pc1:11311/'
alias export_yb3='export ROS_MASTER_URI=http://youbot-brsu-3-pc1:11311/'
alias export_yb4='export ROS_MASTER_URI=http://youbot-brsu-4-pc1:11311/'
```

## See also
* [Tools](wiki/development/toolkit/tools)
* [Using ssh without password](wiki/development/setup/tips)
