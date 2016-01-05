# Ros2Bot 

Ros2Bot is a personnel Robot Kit based on open source platform for Developing Highly capable application like mobile robots through its vision system and mobile base which is empowered by single board compuer.

1. [Quick Guide](#1-quick-guide)

2. [SBC SETUP](https://github.com/GaiTech-Robotics/Ros2Bot/blob/master/Jetson%20Board%20setup.md#2-sbc-setup)

3. [ROS INSTALLATION](https://github.com/GaiTech-Robotics/Ros2Bot/blob/master/ROS%20and%20KINECT2%20installation.md#3-ros-installation)

4. [KINECT2 INSTALLATION](https://github.com/GaiTech-Robotics/Ros2Bot/blob/master/ROS%20and%20KINECT2%20installation.md#4-kinect2-installation)

5. [ROS2BOT MODEL](https://github.com/GaiTech-Robotics/Ros2Bot/blob/master/model/ros2bot_model.md#ros2bot-model-for-your-host-computer-is-provided-by-altering-changes-for-turtlebot-description)


![ROS2BOT MODEL](http://letsmakerobots.com/files/field_primary_image/Screenshot_from_2015-10-23_08_44_48.png?)

![](http://letsmakerobots.com/files/Screenshot_from_2015-10-23_08_44_26.png) 

![](http://letsmakerobots.com/files/Screenshot_from_2015-11-02_07_43_39.png)


##1. Quick Guide

####  1.1 ROS Network Setup
	
	Connect to ROS2BOT to its wifi network which would in the series of ROS2BOT_**** (wifi username & pswd and its default IP provided with the kit). 
	
	
	Before using ROS2BOT, you must configure ROS network in host PC(which you are connecting to ROS2BOT).
	In the host PC add ROS network to your bashrc, in ./bashrc add these lines
	```
		> echo export ROS_HOSTNAME=IP_OF_HOST_PC 
		> echo export ROS_MASTER_URI=http://IP_OF_ROS2BOT:11311
	```
		
	Now turn ON ROS2BOT and connect to it from your host computer

	Note: Currently we have a USB bug with Jetosn sbc board. So please remove USB hub before starting Jetson board. Once started connect the USB hub. While packing the usb of kobuki and kinect might have removed(You can find them next to usb hub). Connect them to the usb ports.
		ssh ubuntu@<IP of ROS2BOT>
	
####  1.2 For ROS2BOT teleop follow these steps
    Open the terminal, connect to ROS2BOT from your host PC 
    
		HOST@HOST-PC$ ssh ubuntu@<IP of ROS2BOT>
		Ubuntu@ros2bot$ roslaunch turtlebot_bringup minimal.launch
		
    In another terminaL :
    
		HOST@HOST-PC$ ssh ubuntu@<IP of ROS2BOT>
		Ubuntu@ros2bot$ roslaunch turtlebot_teleop keyboard_teleop.launch

####  1.3 FOR ROS2BOT navigation, follow these steps:

	Navigation can be done using two methods: OpenGL and CPU method. When compared with CPU method, OpenGL performance is quite good.
####	CPU METHOD
    Open the terminal, connect to ROS2BOT from your host PC 
		
		HOST@HOST-PC$ ssh ubuntu@<IP of ROS2BOT>
		Ubuntu@ros2bot$ roslaunch turtlebot_bringup minimal.launch

    In another terminaL :
		
		HOST@HOST-PC$ ssh ubuntu@<IP of ROS2BOT>
		Ubuntu@ros2bot$ roslaunch turtlebot_navigation gmapping_kinect2_cpu.launch
		
####	OpenGL METHOD
    Open the terminal, connect to ROS2BOT from your host PC 
		
		HOST@HOST-PC$ ssh ubuntu@<IP of ROS2BOT>
		Ubuntu@ros2bot$ roslaunch turtlebot_bringup minimal.launch

    In another terminaL :
		
		HOST@HOST-PC$ ssh ubuntu@<IP of ROS2BOT>
		Ubuntu@ros2bot$ roslaunch turtlebot_navigation gmapping_kinect2_opengl.launch
		
  FOR rviz,
		Open in the host computer
		HOST@HOST-PC$ rviz
		
	Note: You can view ROS2BOT desktop in the host PC by the following way.
	
	In host Pc
	
	$ gvncviewer @<IP of ROS2BOT>
	
	You can install gvncviewer in host PC by using following command
	
	$ sudo apt-get install gvncviewer
	
Note: You can get ROS2BOT model from [here](https://github.com/GaiTech-Robotics/Ros2Bot/blob/master/model/ros2bot_model.md)
	
You can view ROS2BOT desktop in your host pc by the following method

Open the terminal in your host pc and type the following

	$gvncviewer ubuntu@<IP of ros2bot>
	
	if gvncviewer not installed in your host pc , you can install that by using following command
	
	$ sudo apt-get install gvncviewer

####rviz segmentation problem

  Install ros-indigo-robot-model from package manager (which installs geometry dependensies too)
then follow these steps
	$ sudo apt-get remove ros-indigo-robot-model
	
	$ cd ~/catkin_ws/src
	
	$ git clone https://github.com/ros/robot_model.git
	
	$ cd ~/catkin_ws
	
	$ catkin_make
	
	$ source devel/setup.bash

