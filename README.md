# RPG Quadrotor Control

## License

The RPG Quadrotor Control repository provides packages that are intended to be used with [ROS](http://www.ros.org/).
This is research code, expect that it changes often and any fitness for a particular purpose is disclaimed.

The source code is released under a MIT license.
### Installation

* [[Installation Guide|Installation-Guide]]
### Get git
For the following installation instructions you will need git which you can set up with the following commands:
```bash
# in file folder
git config user.name "Your Name Here"
git config user.email "Same e-mail as used for github"
```

### soruce ROS

```bash
 . /opt/ros/noetic/setup.bash
```


### create conda env and Get catkin tools
Get catkin tools with the following commands:
```bash
conda create -n YOURNAME python=3.10
# and make sure you activate conda env when each time you use this project
conda activate YOURNAME # activate conda env 
# python >3.10 will conflict with ros-noetic
pip install catkin-tools
```

### Create a catkin workspace
Create a catkin workspace with the following commands by replacing `<ROS VERSION>` with the actual version of ROS you installed:
```bash
#将所有ros相关源文件放在 src下
catkin build
```

### Set up SSH keys
We strongly recommend to set up ssh keys with github to simplify your workflow. You can do so by following the instructions on [how to set up an ssh key](https://help.github.com/articles/generating-an-ssh-key/). Henceforth, always clone repositories using the ssh url:

[[https://github.com/uzh-rpg/rpg_quadrotor_control/wiki/images/ssh_link.png|alt=ssh_link]]

### Install Dependencies

##### Gazebo
ros have done that

##### ROS Dependencies
Install system and ROS dependencies:
```bash
sudo apt-get install libgoogle-glog-dev protobuf-compiler ros-$ROS_DISTRO-octomap-msgs ros-$ROS_DISTRO-octomap-ros ros-$ROS_DISTRO-joy
```

### Main Installation
Install [vcstool](https://github.com/dirk-thomas/vcstool):
```bash
pip install vcstool
```

Clone dependencies:
```bash
vcs-import < rpg_quadrotor_control/dependencies.yaml
```
Make sure the GUIs in your rqt cache are updated (Don't worry if this outputs an error because the file could not be found, we just want to remove it if it is already there):
```bash
rm ~/.config/ros.org/rqt_gui.ini
```
Build:
```bash
catkin build
```
Add sourcing of your catkin workspace to your `.bashrc` file:
```bash
source ~/.bashrc
```
If you are using the [sbus_bridge](https://github.com/uzh-rpg/rpg_quadrotor_control/tree/master/bridges/sbus_bridge), add your user to the dialout group:
```bash
sudo usermod -aG dialout $USER
```
If you are using GPIO or ADC functionalities from the [rpg_single_board_io](https://github.com/uzh-rpg/rpg_single_board_io) repository, follow the set up instructions in its [readme](https://github.com/uzh-rpg/rpg_single_board_io/blob/master/README.md).

### Test the Framework
To test you installation, follow the [[Test the Framework|Test-the-Framework]] instructions.

## Instructions

Instructions for the installation and usage of this software is provided along with further details in our [Wiki](https://github.com/uzh-rpg/rpg_quadrotor_control/wiki). If you have questions or problems with this framework, please use the [issue tracker](https://github.com/uzh-rpg/rpg_quadrotor_control/issues). Please don't send us emails since they might not be answered. If you would like to contribute, please read the [How to Contribute page](https://github.com/uzh-rpg/rpg_quadrotor_control/wiki/How-to-Contribute) first.

## Summary

This repository contains a complete framework for flying quadrotors based on control algorithms developed by the [Robotics and Perception Group](http://www.ifi.uzh.ch/en/rpg.html).
We also provide an interface to the [RotorS](https://github.com/ethz-asl/rotors_simulator) Gazebo plugins to use our algorithms in simulation.
Together with the provided simple trajectory generation library, this can be used to test our sofware entirely in simulation.
We also provide some utility to command a quadrotor with a gamepad through our framework as well as some calibration routines to compensate for varying battery voltage.
Finally, we provide an interface to communicate with flight controllers used for First-Person-View racing.

The theory behind the included algorithms is summarized in the [theory document](https://github.com/uzh-rpg/rpg_quadrotor_control/blob/master/documents/theory_and_math/theory_and_math.pdf) contained in this repository as well as in our [RA-L18 Paper](http://rpg.ifi.uzh.ch/docs/RAL18_Faessler.pdf) with a technical report attached for further details as well as in our [RA-L17 Paper](http://rpg.ifi.uzh.ch/docs/RAL17_Faessler.pdf).

This repository makes use of some basic functionalities from the [rpg_quadrotor_common](https://github.com/uzh-rpg/rpg_quadrotor_common) repository and when working with real hardware, the GPIO and ADC functionalities in the [rpg_single_board_io](https://github.com/uzh-rpg/rpg_single_board_io) repository might come in handy.

#### Publication

If you use this work in an academic context, please cite the following two RA-L publications:

M. Faessler, A. Franchi, and D. Scaramuzza, 
"**Differential Flatness of Quadrotor Dynamics Subject to Rotor Drag for Accurate Tracking of High-Speed Trajectories**,"
IEEE Robot. Autom. Lett. (RA-L), vol. 3, no. 2, pp. 620–626, Apr. 2018. [[PDF](http://rpg.ifi.uzh.ch/docs/RAL18_Faessler.pdf)]

    @Article{Faessler18ral,
      author        = {Matthias Faessler and Antonio Franchi and Davide Scaramuzza},
      title         = {Differential Flatness of Quadrotor Dynamics Subject to Rotor
                      Drag for Accurate Tracking of High-Speed Trajectories},
      journal       = {{IEEE} Robot. Autom. Lett.},
      year          = 2018,
      volume        = 3,
      number        = 2,
      pages         = {620--626},
      month         = apr,
      doi           = {10.1109/LRA.2017.2776353},
      issn          = {2377-3766}
    }
    
M. Faessler, D. Falanga, and D. Scaramuzza, 
"**Thrust Mixing, Saturation, and Body-Rate Control for Accurate Aggressive Quadrotor Flight**,"
IEEE Robot. Autom. Lett. (RA-L), vol. 2, no. 2, pp. 476–482, Apr. 2017. [[PDF](http://rpg.ifi.uzh.ch/docs/RAL17_Faessler.pdf)]

    @Article{Faessler17ral,
      author        = {Matthias Faessler and Davide Falanga and Davide Scaramuzza},
      title         = {Thrust Mixing, Saturation, and Body-Rate Control for Accurate
                      Aggressive Quadrotor Flight},
      journal       = {{IEEE} Robot. Autom. Lett.},
      year          = 2017,
      volume        = 2,
      number        = 2,
      pages         = {476--482},
      month         = apr,
      doi           = {10.1109/LRA.2016.2640362},
      issn          = {2377-3766}
    }

Watch the [video](https://youtu.be/VIQILwcM5PA) demonstrating what can be done by the control algorithms in this repository:

[![Differential Flatness of Quadrotor Dynamics Subject to Rotor Drag](http://rpg.ifi.uzh.ch/img/quad_control/thumb_1.jpeg)](https://youtu.be/VIQILwcM5PA)

And the [video teaser](https://youtu.be/LmMgx_vKh5s) for our presentation at [ICRA 2018](https://icra2018.org/):

[![ICRA 2018 Video Teaser: Differential Flatness of Quadrotor Dynamics Subject to Rotor Drag](http://rpg.ifi.uzh.ch/img/quad_control/thumb_2.jpeg)](https://youtu.be/LmMgx_vKh5s)