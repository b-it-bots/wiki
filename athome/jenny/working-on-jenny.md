[[_TOC_]]

## ssh to Jenny
In order to be able to compile the repositories in Jenny, you need to add the following to your /etc/hosts file:

```
192.168.1.101 cob3-1-pc1
192.168.1.102 cob3-1-pc2
192.168.1.103 cob3-1-pc3
```

To ssh to Jenny:
```
ssh -X username@cob3-1-pc#
```

where `username` should be replaced by the username of the workstation you are using and `#` by the pc number in Jenny that you want to access. See also [Aliases](setup/aliases)

Now you can follow the instructions in the README files `mas_common_robotics`. For @home you should do the same with the README of `mas_domestic_robotics` and for @work the README in `mas_industrial_robotics`.


## Setting up your user in Jenny
You will need at least four terminals open in your laptop.

1. Look at the [aliases](setup/aliases) section.
2. ssh in each of the PCs by using `cob1`, `cob2`, `cob3`.
2. In each of the PCs, you need to generate shh keys following [these instructions](https://help.github.com/articles/generating-ssh-keys).
1. Add them to GitHub and Gitgate in the ssh keys section.

You may want to take a look at [how to use your ssh key without entering a password](tips#ssh).


## Initializing Jenny
When running code on Jenny, first you need to initialize her. Note that sometimes it may be necessary to run the release the emergency stop procedure before initalizing.

1. First launch the dashboard in your PC:
```
roslaunch mdr_bringup dashboard.launch
```

2. Press `Init all`
3. Press `Recover all`

  Note: You can also use the joystick with the combination: `Dead man + 10`


## Using the joypad for teleop
See [image here](http://wiki.ros.org/cob_teleop).
# See also
* [Aliases](setup/aliases)
