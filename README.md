# ROS_handson
This repo contains the files needed for doing the hands on turtlesim example in Robot Operating System

## Turtlesim Demo Tutorial
This is a tutorial on running the turtlesim node and controlling it using keyboard

### Prerequisites
For this tutorial we'll use a lighweight simulator, to install it run the following command.
For ROS Melodic,
```sh
sudo apt-get install ros-melodic-ros-tutorials
```
For ROS Noetic,
```sh
sudo apt-get install ros-noetic-ros-tutorials
```
### Running turtlesim and teleop node
First, run roscore to initialise the roslaunch server
```sh
roscore
```
Now, open another terminal window start the turtlesim node located in turtlesim package
```sh
rosrun turtlesim turtlesim_node
```
Check if it is running using (Again in a new cmd window):
```sh
rosnode list
```
Now, in a new cmd window run the key teleoperation node which communicates with the turtlesim node through the topic ---
```sh
rosrun turtlesim turtle_teleop_key
```
Keeping this terminal window open, use the arrow keys to move the turtle in various directions
### Analysing the nodes and topics
To see all the currently running nodes, use:
```sh
rosnode list
```
To get info on a certain node (say sample_node),
```sh
rosnode info sample_node
```
To list out the currently active topics,
```sh
rostopic list
```
### Using roslaunch
Instead of calling all the nodes seperately as mentioned above,
we could wrap it all in a .launch file, which can be found in the same repository.
```
<launch>
	<node pkg="turtlesim" name="sim" type="turtlesim_node"/>
	<node pkg="turtlesim" name="sim" type="turtlesim_teleop_key"/>
</launch>
```
Now launch it using one line in the cmd terminal
```sh
roslaunch file.launch
```