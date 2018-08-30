---
title: Running the MAS software

---
Now you can follow the instructions in the README files `mas_common_robotics`. For @home you should do the same with the README of `mas_domestic_robotics` and for @work the README in `mas_industrial_robotics`.

# Summer Camp 2017

After following the instructions for [getting started](/setup/getting-started), you should clone the summer camp repository to your workspace:

```shell
cd ~/kinetic/src
git clone gitgate@mas.b-it-center.de:b-it-bots/summer_2017.git
```

Source your catkin workspace

```shell
source ~/kinetic/devel/setup.bash
```

The last command should be added to the ~/.bashrc file so that they do not need to be executed everytime you open a new terminal.


And finally compile the repository:

```shell
cd ~/kinetic
catkin build
```
