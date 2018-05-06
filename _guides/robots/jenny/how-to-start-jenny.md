# Starting up Jenny

## In PC1
1. Access the first PC of Jenny from the computer by using the command

    ```shell
    ssh -X username@cob3-1-pc1
    ```

 **Alias:** `cob1`.

2. Start the `roscore` using the command

    ```shell
    roscore
    ```

### Bringing up the robot
1. Access Jenny'S PC1 using ssh (alias **cob1**).

2. Bring up the robot using the following command:

    ```shell
    roslaunch mdr_bringup robot.launch
    ```

    **Alias:** `bringup`


## In your PC

1. Open a second terminal and in order to tell your computer where the ROS master is located, set the variable `ROS_MASTER_URI` to Jenny's first PC:

    ```shell
    export ROS_MASTER_URI=http://cob3-1-pc1:11311/
    ```

    **Alias:** `export_cob`

2. To let the ROS master know where youre node is running, set the `ROS_IP` variable to the IP of the PC you are using

    ```shell
    export ROS_IP=<Your IP address>
    ```

    **Alias:** `export_rosip`

    Note: The `ifconfig` command can be used to get your computer's IP address.

3. Launch the "Dashboard" GUI, used to initialize Jenny

```shell
roslaunch mdr_bringup dashboard.launch
```
**Alias:** `dashboard`



### In the Dashboard GUI

1. First click on "**Init all**" button in the GUI  
Note: Emergency switches have to be released ( [procedure for releasing the emergency switch](https://mas.b-it-center.de/gitgate/b-it-bots/bitbots_athome/wikis/jenny/turning-jenny-on-and-off) ) before the pressing "Init all"

 The wheels will rotate above its z axis and the torso and camera will move to its initial position.

2. Then click **Recover all**  
After few seconds check mark on the GUI should be green


# Turning off the computers in Jenny

Access each of the PCs in Jenny (alias `cob1`, `cob2`, `cob3`) and shut down the computer

```shell
sudo shutdown now
```

Note: for all the alias list click [here](wiki/development/setup/aliases)
