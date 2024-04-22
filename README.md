# Reasoning Messages

## Overview

Reasoning Messages stores msg and srv definitinos for reasoning tasks on S-Graphs.

### License

The source code is released under GPLv3 License [![License: GPLv3](https://img.shields.io/badge/License-GPLv3-yellow.svg)](https://opensource.org/license/gpl-3-0).

**Author: Jose Andres Millan Romera<br />
Affiliation: [University of Luxembourg](https://www.anybotics.com/)<br />
Maintainer: Jose Andres Millan Romera, josmilrom@gmail.com**

The ROS 2 graph_manager messages package has been tested under [ROS2] Humble on Ubuntu 20.04.
This is research code, expect that it changes often and any fitness for a particular purpose is disclaimed.

## Messages

**Match**
- name [string]
- basis_nodes [Node[]]
- target_nodes [Node[]]
- edges [Edge[]]

**Graph**
- name [string]
- nodes [Node[]]
- edges [Edge[]]

**Node**
- id [int32]
- type [string]
- attributes [Attribute[]]

**Edge**
- origin_node [int64]
- target_node [int64]
- attributes [Attribute[]]

**Attribute**
- name [string]
- str_value [string]
- fl_value [float64[]]


## Installation

### Installation from Packages

The only tested ROS version for this package is ROS2 Humble
    

#### Building

To build from source, clone the latest version from this repository into your catkin workspace and compile the package using

	cd catkin_workspace/src
	git clone https://github.com/snt-arg/ros2_graph_manager_msgs.git
	cd ../
	colcon build


## ROS1 Bridge

Find instructions in https://github.com/ros2/ros1_bridge

Clone the repo in the ROS2 WP or a new WP.

### Building from source

Build the ROS 1 messages:


```bash
# Shell A (ROS 1 only):
cd <path-to-ros1-ws>
catkin build
```

Build the ROS 2 messages:

```bash
# Shell B (ROS 2 only):
cd <path-to-ros2-ws>
colcon build --symlink-install --packages-skip ros1_bridge
```


Build the bridge:

```bash
# Shell C (ROS 1 + ROS 2):
export ROS1_INSTALL_PATH=<install-space-to-ros1 >
export ROS2_INSTALL_PATH=<install-space-to-ros2 >
source ${ROS1_INSTALL_PATH}/setup.bash
source <install-space-to-ros1-overlay-ws>/setup.bash
source ${ROS2_INSTALL_PATH}/setup.bash
source <install-space-to-ros2-overlay-ws>/local_setup.bash

cd <bridge-ws>
colcon build --symlink-install --packages-select ros1_bridge --cmake-force-configure

```

Verify the custom messages

```bash
ros2 run ros1_bridge dynamic_bridge --print-pairs | grep reasoning_msgs
```


### Usage

First we start a ROS 1 `roscore`:


```bash
# Shell A (ROS 1 only):
source ${ROS1_INSTALL_PATH}/setup.bash
roscore
```

Then we start the dynamic bridge 


```bash
# Shell B (ROS 1 + ROS 2):
# Source ROS 1 first:
source ${ROS1_INSTALL_PATH}/setup.bash
# Source ROS 2 next:
source ${ROS2_INSTALL_PATH}/setup.bash
export ROS_MASTER_URI=http://localhost:11311
ros2 run ros1_bridge dynamic_bridge
```

Now we start the ROS 1 nodes.


```bash
# Shell C:
source ${ROS1_INSTALL_PATH}/setup.bash
roslaunch ...
```


Now we start the ROS 2 nodes


```bash
# Shell D:
source ${ROS2_INSTALL_PATH}/setup.bash
ros2 launch ...
```








