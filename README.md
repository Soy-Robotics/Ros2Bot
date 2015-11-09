# Ros2Bot 

Ros2Bot is a personnel Robot Kit based on open source platform for Developing Highly capable application like mobile robots through its vision system and mobile base which is empowered by single board compuer.

	1.SBC SETUP

	2.ROS INSTALLATION

	3.KINECT2 INSTALLATION

	4.REPLACING FILES FOR ROS2BOT MODEL

1.SBC SETUP

Jetson TK1 is used as single board computer. The board configurations are following
	2.3 GHz , quad core processor
	2 GB ram
	16 GB inbuilt memory

OS installation
	Jetson TK1 board comes with Tegra-Linux-R19.3. I have encountered several problems using this version especially desktop management and login loop problem. Hence chosen Tegra-Linux-R21.3 version.

1. flash the os from this link and use downloaded files- follow the instructions

   https://devtalk.nvidia.com/default/topic/823132/-customkernel-the-grinch-21-3-4-for-jetson-tk1-developed/

   wget http://developer.download.nvidia.com/embedded/L4T/r21_Release_v3.0/Tegra124_Linux_R21.3.0_armhf.tbz2

   wget http://developer.download.nvidia.com/embedded/L4T/r21_Release_v3.0/Tegra_Linux_Sample-Root-Filesystem_R21.3.0_armhf.tbz2

2 . after downloading these files follow these instruciton in the host computer
	1 tar -xvf Tegra124_Linux_R21.3.0_armhf.tbz2
	2 cd Linux_for_Tegra/rootfs
	3 sudo tar xpf ../../Tegra_Linux_Sample-Root-Filesystem_R21.3.0_armhf.tbz2
	4 cd ..
	5.sudo ./apply_binaries.sh

3. Now flash the os into the board by connecting the board in recovery mode
	1. sudo ./flash.sh jetson-tk1 mmcblk0p1
	2. reboot the jetson board 

Kernal installation steps
1. Download following files
  1. wget http://www.jarzebski.pl/files/jetsontk1/grinch-21.3.4/zImage
  2. wget http://www.jarzebski.pl/files/jetsontk1/grinch-21.3.4/jetson-tk1-grinch-21.3.4-modules.tar.bz2
  3. wget http://www.jarzebski.pl/files/jetsontk1/grinch-21.3.4/jetson-tk1-grinch-21.3.4-firmware.tar.bz2
 
  

2. check for the avialability of files, to do so follow these instructions
	$ md5sum zImage 
  	a4a4ea10f2fe74fbb6b10eb2a3ad5409  zImage
	$ md5sum jetson-tk1-grinch-21.3.4-modules.tar.bz2 
 	  3f84d425a13930af681cc463ad4cf3e6  jetson-tk1-grinch-21.3.4-modules.tar.bz2
	$ md5sum jetson-tk1-grinch-21.3.4-firmware.tar.bz2
 	  f80d37ca6ae31d03e86707ce0943eb7f  jetson-tk1-grinch-21.3.4-firmware.tar.bz2


3. now update the kernal
	$ sudo tar -C /lib/modules -vxjf jetson-tk1-grinch-21.3.4-modules.tar.bz2
	$ sudo tar -C /lib -vxjf jetson-tk1-grinch-21.3.4-firmware.tar.bz2
	$ sudo cp zImage /boot/zImage
      check the kernal by connecting turtlebot usb and see whether u can find USB0. If so you are successfully finished the installation.


Now jetson board has been configured with ubuntu environment
To install CUDA on Jetson TK1 - L4T System



Execute the following commands:
  $ sudo dpkg -i cuda-repo-<distro>_<version>_<architecture>.deb
  $ sudo apt-get update
  $ sudo apt-get install cuda-toolkit-6-5


#Ros Installation
turn all the servers on in software and updates under ubuntu software tab
check all under updates tab in software and updates
1. Follow
	http://wiki.ros.org/NvidiaJetsonTK1
Set your Locale
sudo update-locale LANG=C LANGUAGE=C LC_ALL=C LC_MESSAGES=POSIX
Setup your sources.list
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'
Set up your keys
wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -
Installation
sudo apt-get update
sudo apt-get install ros-indigo-ros-base
Initialize rosdep
sudo apt-get install python-rosdep
sudo rosdep init
rosdep update
Environment setup
echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
source ~/.bashrc
Getting rosinstall
sudo apt-get install python-rosinstall

to avoid rviz segfault 
in ~/.bashrc:
unset GTK_IM_MODULE

Turtlebot installation
1.download from synaptic package manager
2. install remaining from here packag http://wiki.ros.org/turtlebot/Tutorials/indigo/Turtlebot%20Installation
or 
sudo apt-get install ros-indigo-turtlebot ros-indigo-turtlebot-apps ros-indigo-turtlebot-interactions ros-indigo-turtlebot-simulator ros-indigo-kobuki-ftdi ros-indigo-rocon-remocon ros-indigo-rocon -qt-library ros-indigo-ar-track-alvar-msgs
3. change from create to kobuki in minimal.launch
4. add export in .bashrc "export TURTLEBOT_BASE = kobuki"
5. rosrun kobuki_ftdi create_dev_rules 
kinect installation:
1. add "export TURTLEBOT_3D_SENSOR = kinect" in bashrc

creating catkin workspace
change workspace to catkin_Ws/devel/setup.bash in ~/.bashrc

installing xlz/libfreenect2 in home folder

install libfreenect2 from openk inect/libfreenect2 in downloads folder
changed usb_port_owner_inf=2 from 0
sudo permissions from autosuspend
install kinect2birdge

check in all the libusb path by typing ldd in their path 

remove the kinec2 cable, restart the system
After reboot  check for kinect2 inputs by typing lsusb
in downloads/libfreenect2/rules/90-kinect rules, edit according to your kinect2 usb configuration and copy the file to /etc/udev/rules
copy all the kinect2files which are available in email

rviz robot model
$ sudo apt-get remove ros-indigo-robot-model
$ cd ~/catkin_ws/src
$ git clone https://github.com/ros/robot_model.git
$ cd ~/catkin_ws
$ catkin_make
$ source devel/setup.bash
install ros-indigo-robot-model


in hostmachine , kinect2 glfw problem sovled after changing depth_method from opengl to cpu
