# Ros2Bot 

Ros2Bot is a personnel Robot Kit based on open source platform for Developing Highly capable application like mobile robots through its vision system and mobile base which is empowered by single board compuer.

1. [Quick Guide](#1-quick-guide)

2. [SBC SETUP](#2-sbc-setup)

3. [ROS INSTALLATION](#3-ros-installation)

4. [KINECT2 INSTALLATION](#4-kinect2-installation)

5. [REPLACING FILES FOR ROS2BOT MODEL](#5-replace-these-following-files)


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
	
	

## 3. ROS INSTALLATION

####3.1 Installation Steps
Turn on all the servers in software and updates under ubuntu software tab. Check all under updates tab in software and updates

	http://wiki.ros.org/NvidiaJetsonTK1

-Set your Locale

	$ sudo update-locale LANG=C LANGUAGE=C LC_ALL=C LC_MESSAGES=POSIX
	
-Setup your sources.list

	$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'
	
-Set up your keys

	$wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -

- Installation

	$ sudo apt-get update
	
	$ sudo apt-get install ros-indigo-ros-base

- Initialize rosdep

	$ sudo apt-get install python-rosdep

	$ sudo rosdep init

	$ rosdep update

- Environment setup

	$ echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc

	$ source ~/.bashrc

- Getting rosinstall

	$ sudo apt-get install python-rosinstall

- To avoid rviz segfault, in ~/.bashrc:

	echo "unset GTK_IM_MODULE" >>~/.bashrc

- Let's create a catkin workspace:

	$ mkdir -p ~/catkin_ws/src

	$ cd ~/catkin_ws/src
	
	$ catkin_init_workspace


Even though the workspace is empty (there are no packages in the 'src' folder, just a single CMakeLists.txt link) you can still "build" the workspace:

	$ cd ~/catkin_ws/

	$ catkin_make

change the environment to catkin_Ws/devel/setup.bash in ~/.bashrc

#####3.2 Turtlebot installation

$ sudo apt-get install ros-indigo-turtlebot ros-indigo-turtlebot-apps ros-indigo-turtlebot-interactions ros-indigo-kobuki-ftdi ros-indigo-rocon-remocon ros-indigo-rocon-qt-library ros-indigo-ar-track-alvar-msgs

- Change from create to kobuki in minimal.launch at turtlebot_bringup/launch

- echo  "export TURTLEBOT_BASE=kobuki" >>~/.bashrc

- $ rosrun kobuki_ftdi create_udev_rules 

- echo "export TURTLEBOT_3D_SENSOR=kinect2" >>~/.bashrc

##4. kinect2 installation

####4.1 Installing cuda based libfreenect2 in home folder

	$ cd ~
	
	$ git clone https://github.com/GaiTech-Robotics/libfreenect2

	$ sudo apt-get install -y build-essential libturbojpeg libtool autoconf libudev-dev cmake mesa-common-dev freeglut3-dev libxrandr-dev doxygen libxi-dev libjpeg-turbo8-dev
	
	$ cd libfreenect2/depends

	$ sh install_ubuntu.sh
	
	$ sudo ln -s /usr/lib/arm-linux-gnueabihf/libturbojpeg.so.0.0.0 /usr/lib/arm-linux-gnueabihf/libturbojpeg.so
	
	$ cd ../examples/protonect/
	
	$ mkdir build && cd build
	
	$ cmake ..
	
	$ make 
	
	$ sudo make install

####4.2 Installing libfreenect2 in Download folder
	$ cd Downloads/
	
	$ git clone https://github.com/OpenKinect/libfreenect2.git
	
	$ sudo apt-get install build-essential cmake pkg-config libturbojpeg libjpeg-turbo8-dev mesa-common-dev freeglut3-dev libxrandr-dev libxi-dev
	
	$ cd libfreenect2/depends
	
	$ sh install_ubuntu.sh
	
	$ sh install_libusb.sh
	
	$ cd ../
	
	$ mkdir build && cd build
	
	$ cmake ..
	
	$ make
	
	$ sudo make install


####4.3 Install kinect2 bridge

	$ cd ~/catkin_ws/src/
	
	$ git clone https://github.com/code-iai/iai_kinect2.git
	
	$ cd iai_kinect2
	
	$ rosdep install -r --from-paths .
	
	$ cd ~/catkin_ws
	
	$ catkin_make -DCMAKE_BUILD_TYPE="Release"

- USB 3.0 must be enabled for full performance. Edit /boot/extlinux/extlinux.conf to change usb_port_owner_info=0 to usb_port_owner_info=2 to enable USB 3.0.

	$ sudo -s
	
	$ sudo gedit /boot/extlinux/extlinux.conf

- Now change "usb_port_owner_info=0" to "usb_port_owner_info=2"

-You must have read and write permissions on the USB devices of Kinect 2.

- lsusb to find out the bus id and device id of Kinect 2 (there should be 3 devices).
- ls -l /dev/bus/usb/$BUS_ID/$DEVICE_ID and you should have rw permissions. To make it permanent, you can create a udev rule /etc/udev/rules.d/90-kinect2.rules. Add these lines in it.

ATTR{product}=="Kinect2"

	SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02c4", MODE="0666"
	
	SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02d8", MODE="0666"
	
	SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02d9", MODE="0666"

-Now remove the kinec2 cable, restart the system After reboot check for kinect2 inputs by typing lsusb


####rviz segmentation problem

  Install ros-indigo-robot-model from package manager (which installs geometry dependensies too)
then follow these steps
	$ sudo apt-get remove ros-indigo-robot-model
	
	$ cd ~/catkin_ws/src
	
	$ git clone https://github.com/ros/robot_model.git
	
	$ cd ~/catkin_ws
	
	$ catkin_make
	
	$ source devel/setup.bash


##replace these following files
TODO

in hostmachine , kinect2 glfw problem sovled after changing depth_method from opengl to cpu
