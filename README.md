# Ros2Bot 

Ros2Bot is a personnel Robot Kit based on open source platform for Developing Highly capable application like mobile robots through its vision system and mobile base which is empowered by single board compuer.

- [SBC SETUP](#sbc-setup)


- [ROS INSTALLATION](#ros-installation)

- [KINECT2 INSTALLATION](#kinect2-installation)

- REPLACING FILES FOR ROS2BOT MODEL

##SBC SETUP

	Jetson TK1 is used as single board computer. The board configurations are following
	2.3 GHz , quad core processor
	2 GB ram
	16 GB inbuilt memory

OS installation
	Jetson TK1 board comes with Tegra-Linux-R19.3. I have encountered several problems using this version especially desktop management and login loop problem. Hence chosen Tegra-Linux-R21.3 version.
Follow these steps in host computer


Before you Begin
> You have a Jetson TK1 Tegra Developer Kit equipped with the NVIDIA Tegra K1 processor.
> You have a host machine that is running Linux.
> Your developer system is cabled as follows:
	->Serial cable plugged into the serial port J1A2 UART4 on the target connected to your Linux host directly or through a serial-to-USB converter. (To setup serial console on the Linux host.)
	-> USB Micro-B cable connecting Jetson TK1 (J1E1 USB0) to your Linux host for flashing.
	-> A USB hub should be connected to the USB port (J1C2 USB2) on the Jetson TK1 system.
	-> An HDMI cable plugged into "J1C1 HDMI1" on the target which is connected to an external HDMI display.
	-> An Ethernet cable plugged into the J1D1 on board Ethernet port.


1. flash the os from this link and use downloaded files- follow the instructions

   https://devtalk.nvidia.com/default/topic/823132/-customkernel-the-grinch-21-3-4-for-jetson-tk1-developed/

   wget http://developer.download.nvidia.com/embedded/L4T/r21_Release_v3.0/Tegra124_Linux_R21.3.0_armhf.tbz2

   wget http://developer.download.nvidia.com/embedded/L4T/r21_Release_v3.0/Tegra_Linux_Sample-Root-Filesystem_R21.3.0_armhf.tbz2

2 . after downloading these files follow these instruciton in the host computer. In the terminal,
	$ tar -xvf Tegra124_Linux_R21.3.0_armhf.tbz2
	$ cd Linux_for_Tegra/rootfs
	$ sudo tar xpf ../../Tegra_Linux_Sample-Root-Filesystem_R21.3.0_armhf.tbz2
	$ cd ..
	$.sudo ./apply_binaries.sh

3. Now flash the os into the board by connecting the board to host computer in recovery mode.(connect the usb cable and now press the reset button by holding recovery button on jetson board)
	1. sudo ./flash.sh jetson-tk1 mmcblk0p1
	2. reboot the jetson board 
-Now you will see ubuntu environment in the jetson system.

Kernal installation steps(Follow these steps in jetson board)
1. Download following files
  1. wget http://www.jarzebski.pl/files/jetsontk1/grinch-21.3.4/zImage
  2. wget http://www.jarzebski.pl/files/jetsontk1/grinch-21.3.4/jetson-tk1-grinch-21.3.4-modules.tar.bz2
  3. wget http://www.jarzebski.pl/files/jetsontk1/grinch-21.3.4/jetson-tk1-grinch-21.3.4-firmware.tar.bz2
  
2. check for the avialability of files, to do so follow these instructions in the terminal
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


Download cuda kit from the following link
http://developer.download.nvidia.com/embedded/L4T/r21_Release_v3.0/cuda-repo-l4t-r21.3-6-5-prod_6.5-42_armhf.deb

Execute the following commands in the terminal:
  $ cd /path to cuda package
  $ sudo dpkg -i cuda-repo-<distro>_<version>_<architecture>.deb
  $ sudo apt-get update
  $ sudo apt-get install cuda-toolkit-6-5


## ROS INSTALLATION

Turn on all the servers in software and updates under ubuntu software tab. Check all under updates tab in software and updates
1. Follow
	http://wiki.ros.org/NvidiaJetsonTK1
-Set your Locale
	$ sudo update-locale LANG=C LANGUAGE=C LC_ALL=C LC_MESSAGES=POSIX
-Setup your sources.list
	$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'
-Set up your keys
	$wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -

Installation
	$ sudo apt-get update
	$ sudo apt-get install ros-indigo-ros-base

Initialize rosdep
	$ sudo apt-get install python-rosdep
	$ sudo rosdep init
	$ rosdep update

Environment setup
	$ echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
	$ source ~/.bashrc

Getting rosinstall
	$ sudo apt-get install python-rosinstall

To avoid rviz segfault 
in ~/.bashrc:
	unset GTK_IM_MODULE

Let's create a catkin workspace:

$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/src
$ catkin_init_workspace

Even though the workspace is empty (there are no packages in the 'src' folder, just a single CMakeLists.txt link) you can still "build" the workspace:

$ cd ~/catkin_ws/
$ catkin_make

change the environment to catkin_Ws/devel/setup.bash in ~/.bashrc

Turtlebot installation
$ sudo apt-get install ros-indigo-turtlebot ros-indigo-turtlebot-apps ros-indigo-turtlebot-interactions ros-indigo-turtlebot-simulator ros-indigo-kobuki-ftdi ros-indigo-rocon-remocon ros-indigo-rocon -qt-library ros-indigo-ar-track-alvar-msgs
- change from create to kobuki in minimal.launch
- add export in .bashrc "export TURTLEBOT_BASE = kobuki"
- rosrun kobuki_ftdi create_dev_rules 
- add "export TURTLEBOT_3D_SENSOR = kinect2" in bashrc

##kinect2 installation

installing cuda based libfreenect2 in home folder

https://github.com/GaiTech-Robotics/libfreenect2
sudo apt-get install -y build-essential libturbojpeg libtool autoconf libudev-dev cmake mesa-common-dev freeglut3-dev libxrandr-dev doxygen libxi-dev libjpeg-turbo8-dev
cd libfreenect2/depends
sh install_ubuntu.sh
sudo ln -s /usr/lib/arm-linux-gnueabihf/libturbojpeg.so.0.0.0 /usr/lib/arm-linux-gnueabihf/libturbojpeg.so
cd ../examples/protonect/
mkdir build && cd build
cmake ..
make 
sudo make install

Installing libfreenect2 in Download folder
$ cd Downloads/
$ 






install libfreenect2 from openk inect/libfreenect2 in downloads folder
changed usb_port_owner_inf=2 from 0
sudo permissions from autosuspend
install kinect2birdge
https://github.com/code-iai/iai_kinect2


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
