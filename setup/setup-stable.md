# Setup And Install A Seperated, Stable Workspace

Motivation: move repositories which are rarely modified to a separated location to avoid building them everytime with your `$ROS_WORKSPACE`.

## Presiquisites

* Clean [ROS install](http://wiki.ros.org/indigo/Installation)
* `python-wstool` and `python-catkin-tools` installed (this guide uses command from catkin_tools, i.e.`catkin build` instead of `catkin_make`)

```bash
sudo apt install python-wstool python-catkin-tools
```

* Open a terminal without any `setup.bash` sourced, i.e. `env | grep -i` ros should print nothing (if not use `unset` or edit `.bashrc` file).
* Clone [`ros-stable-ws-setup`](https://mas.b-it-center.de/gitgate/mnguy12s/ros-stable-ws-setup)

```bash
export WS_SETUP_PATH=/path/to/my/ws/setup   # i.e. ~/ros-ws-setup
git clone gitgate@mas.b-it-center.de:mnguy12s/ros-stable-ws-setup.git $WS_SETUP_PATH
```

Note: for `zsh` users, source `setup.zsh` instead of `setup.bash` for all workspaces

## Install stable workspace

### Run `repositories.debs`
The easiest way to install all packages required by the @Home repositories is to execute the `repositories.debs` file in [mas_domestic_robotics](https://mas.b-it-center.de/gitgate/mas-group/mas_domestic_robotics) repository. This however requires some modification to the script in order to avoid conflict with the stable workspace setup:
* Clone the MAS repositories first to get the `repositories.debs`. The `wstool` command should create the `src` directory with three `mas_*` repositories.

```bash
export MAS_WORKSPACE_PATH=/path/to/mas/ws   # i.e. ~/catkin_ws/indigo
mkdir -p $MAS_WORKSPACE_PATH
cd $MAS_WORKSPACE_PATH
wstool init src $WS_SETUP_PATH/cob-user/mas-domestic-robotics.rosinstall
```

* Edit the `repositories.debs` under the `mas_domestic_robotics` directory:

```bash
cd src/mas_domestic_robotics
vim repositories.debs   # or emacs, nano
```

  * Comment out `rosinstall .. /opt/ros/indigo repository.rosinstall` line (these repositories will be installed with the stable workspace).
  * `ros-indigo-cob-extern` in `packagelist` will cause errors with `apt` installation (messages about overwriting some README files), so comment it out or resolve this in some other way.
* Execute `repositories.debs`

```bash
./repositories.debs
```

### Configure and build stable workspace
* Configure stable workspace

```bash
source /opt/ros/indigo/setup.bash                 # get cakin commands
export STABLE_WORKSPACE_PATH=/path/to/stable/ws   # i.e. ~/catkin_ws/indigo-cob3-1-stable
mkdir -p $STABLE_WORKSPACE_PATH
cd $STABLE_WORKSPACE_PATH
wstool init src $WS_SETUP_PATH/cob-stable/indigo-cob3-1-stable-pc2.rosinstall
catkin config --init
catkin config --install --install-space /opt/ros/indigo-cob3-1-stable
```

* Run `catkin config` in `$STABLE_WORKSPACE_PATH` to check workspace configuration. The output should have the correct `Extending` and `Install Space` paths:

```
Extending:          [cached] /opt/ros/indigo
Workspace:                   $STABLE_WORKSPACE_PATH
----------------------------------------------------------------------------
Source Space:       [exists] $STABLE_WORKSPACE_PATH/src
Log Space:          [exists] $STABLE_WORKSPACE_PATH/logs
Build Space:        [exists] $STABLE_WORKSPACE_PATH/build
Devel Space:        [exists] $STABLE_WORKSPACE_PATH/devel
Install Space:      [exists] /opt/ros/indigo-cob3-1-stable
```

* If workspace configuration is okay, build stable workspace by running `catkin build`

## Configure and build MAS workspace
* This will be your development workspace with the `mas_*` repositories.

```bash
cd $MAS_WORKSPACE_PATH
source /opt/ros/indigo-cob3-1-stable/setup.bash     # make MAS workspace extends
                                                    # the stable workspace
catkin config --init
```

* Check workspace configuration by running `catkin config`, the output should have the correct `Extending` path:

```
Extending:          [cached] /opt/ros/indigo-cob3-1-stable:/opt/ros/indigo
Workspace:                   $MAS_WORKSPACE_PATH
--------------------------------------------------------------------------
Source Space:       [exists] $MAS_WORKSPACE_PATH/src
Log Space:          [exists] $MAS_WORKSPACE_PATH/logs
Build Space:        [exists] $MAS_WORKSPACE_PATH/build
Devel Space:        [exists] $MAS_WORKSPACE_PATH/devel
Install Space:      [unused] $MAS_WORKSPACE_PATH/install
```