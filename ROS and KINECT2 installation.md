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

