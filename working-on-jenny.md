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
ssh username@cob3-1-pc#
```

where `username` should be replaced by the username of the workstation you are using and `#` by the pc number in Jenny that you want to access. See also [Aliases](aliases)

Now you can follow the instructions in the README files `mas_common_robotics`. For @home you should do the same with the README of `mas_domestic_robotics` and for @work the README in `mas_industrial_robotics`.


## Initializing Jenny
When running code on Jenny, first you need to initialize her. Note that sometimes it may be necessary to run the release the emergency stop procedure before initalizing.

1. First launch the dashboard:
```
roslaunch mdr_bringup dashboard.launch
```

2. Press `Init all`
3. Press `Recover all`

  Note: You can also use the joystick with the combination: `Dead man + 10`

# See also
* Aliases (aliases)
