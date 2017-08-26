# Starting up the Jenny
- Open a **terminal** in Ubuntu from the PC that is connected to the Jenny

* Access the first PC of Jenny from the computer by using the command "ssh -X username@cob3-1-pc1" (Alias **cob1**)

Note: for all the alias list [Aliases] (https://mas.b-it-center.de/gitgate/b-it-bots/bitbots_athome/wikis/development/setup/aliases)

* Then start the roscore using the command "**roscore**"

- Open the **second terminal**

* Locate the master using the command " export ROS_MASTER_URI=http://cob3-1-pc1:11311/ " (alias **export_cob**)

* Set the IP address of the PC using the command "export ROS_MASTER_URI=http://cob3-1-pc1:11311/" (alias **export_rosip**)
Note: "ifconfig" command will display all the information about the IP address of the PC

* Launch the "Dashboard" GUI which is used to control the Jenny robot using the command "Roslaunch mdr_bringup dashboard.launch " (alias **dashboard**)

* Open the **third terminal**

* Access the Jenny from the computer you can use the command "ssh -X username@cob3-1-pc1" (Alias **cob1**)

* Launch the "bringup" file using the command  "mdr_bringup robot.launch" (alias **bringup**)

### In the Dashboard GUI

* First click on "**Init all**" button in the GUI

Note: Emergency switches have to be released ( [procedure for releasing the emergency switch] (https://mas.b-it-center.de/gitgate/b-it-bots/bitbots_athome/wikis/jenny/turning-jenny-on-and-off) ) before the pressing "Init all"

* Check for wheels (wheels will rotate above its z axis symbolizing the initialization is done properly)

* Then click **recover all**

* After few seconds check mark on the GUI should be green

* Now the robot is all set for navigation


### Turning off the computer in the robot

* Access the First PC of Jenny  (alias cob1)
* Shut down the computer using the alias **sudo shutdown now**

* Access the Second PC of Jenny (alias cob2)
* Shut down the computer using the alias **sudo shutdown now**

* Access the Third PC of Jenny (alias cob3)
* Shut down the computer using the alias **sudo shutdown now**
