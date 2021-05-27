## Turtlesim Demo Tutorial
This is a tutorial on running the turtlesim node and controlling it using keyboard
It is intended to give you a basic idea of ROS nodes,topics and how publishers and subscribers work

### Prerequisites
For this tutorial we'll use a lighweight simulator, to install it run the following command.
For **ROS Melodic**,
```sh
sudo apt-get install ros-melodic-ros-tutorials
```
For **ROS Noetic**,
```sh
sudo apt-get install ros-noetic-ros-tutorials
```
### Running turtlesim and teleop node
First, run roscore to initialise the master
```sh
roscore
```
Now, open another terminal window.
Start the turtlesim node located in turtlesim package
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

## Using catkin workspace and roslaunch
The above method may not be viable for your future ROS projects. Usually we make a workspace in which we store all our required packages,dependencies,nodes etc. 
### Creating and Building packages
Go to src folder and create the package with the required dependencies
```sh
cd ~/catkin_ws/src
catkin_create_pkg sample_pkg turtlesim
```
Build the newly created package
```sh
cd ~/catkin_ws
catkin build
```
Add 'source devel/setup.bash' to the bashrc, and source it.
```sh
echo 'source devel/setup.bash' >> ~/.bashrc
source ~/.bashrc
```
### Creating and using launch file
Once the package is built correctly,let us create the launch file
```sh
cd ~/catkin_ws/src/sample
mkdir launch
cd launch
touch turtlesim.launch
gedit turtlesim.launch
```
This should open a text editor.Paste the following code in it:
```
<launch>
	<node pkg="turtlesim" name="turtlesim" type="turtlesim_node"/>
	<node pkg="turtlesim" name="teleop" type="turtle_teleop_key"/>
</launch>
```
Save and close the editor.
Now let us launch the nodes!
```sh
cd ~/catkin_ws
roslaunch sample turtlesim.launch
```
The turtlesim window will popup with the turtle at the center. Use the arrow keys to move the turtle.
### Analysing the nodes and topics
To see all the currently running nodes, use:
```sh
rosnode list
```
To get info on a node(say the turtlesim node),
```sh
rosnode info turtlesim
```
To list out the currently active topics,
```sh
rostopic list
```
Observe the messages being published in the **/turtle1/cmd_vel** topic using:
```sh
rostopic echo /turtle1/cmd_vel
```
Click ctrl+C and observe the messages that were being published continuously
```
linear: 
  x: 2.0
  y: 0.0
  z: 0.0
angular: 
  x: 0.0
  y: 0.0
  z: 0.0
```
The above message is of type **geometry_msgs/Twist**, which contains 6 parameters that represent the turtle's linear and angular velocity at each instant
We can also publish a message manually from the command line using rostopic pub [topic] [msg_type] [args]
Execute the following command and see what happens to the turtle
```
rostopic pub -1 /turtle1/cmd_vel geometry_msgs/Twist -- '[2.0, 0.0, 0.0]' '[0.0, 0.0, 7.2]'
```
Likewise, try to move the turtle in the y-direction or rotate it on axis other than z and see what you get :)

Awesome! You've successfully completed the turtlesim tutorial.