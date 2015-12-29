## SBC SETUP

	Jetson TK1 is used as single board computer. The board configurations are following
	2.3 GHz , quad core processor
	2 GB ram
	16 GB inbuilt memory

#####2.1 OS installation
	Jetson TK1 board comes with Tegra-Linux-R19.3. I have encountered several problems using this version especially desktop management and login loop problem. Hence chosen Tegra-Linux-R21.3 version.
Follow these steps in host computer


#####2.1.1 Before you Begin
- You have a Jetson TK1 Tegra Developer Kit equipped with the NVIDIA Tegra K1 processor.

- You have a host machine that is running Linux.

- Your developer system is cabled as follows:

	

		-> USB Micro-B cable connecting Jetson TK1 (J1E1 USB0) to your Linux host for flashing.

		-> A USB hub should be connected to the USB port (J1C2 USB2) on the Jetson TK1 system.

		-> An HDMI cable plugged into "J1C1 HDMI1" on the target which is connected to an external HDMI display.

		-> An Ethernet cable plugged into the J1D1 on board Ethernet port.


#####2.1.2 Get Jetson packages

  -Download Jetson packages in your host computer from the following 
  	
  	$ cd 
  
  	$ wget http://developer.download.nvidia.com/embedded/L4T/r21_Release_v3.0/Tegra124_Linux_R21.3.0_armhf.tbz2

	$ wget http://developer.download.nvidia.com/embedded/L4T/r21_Release_v3.0/Tegra_Linux_Sample-Root-Filesystem_R21.3.0_armhf.tbz2

#####2.1.3 Extracting Jetson packages
  After downloading the files, to extract them follow these instrucitons (in the host computer). In the terminal,

	$ tar -xvf Tegra124_Linux_R21.3.0_armhf.tbz2

	$ cd Linux_for_Tegra/rootfs

	$ sudo tar xpf ../../Tegra_Linux_Sample-Root-Filesystem_R21.3.0_armhf.tbz2

	$ cd ..

	$.sudo ./apply_binaries.sh

#####2.1.4 Flash OS to Jetson board
  
  Now flash the os into the Jetson board by connecting the board to host computer in recovery mode.(connect the usb cable and now press the reset button by holding recovery button on jetson board).

	$ sudo ./flash.sh jetson-tk1 mmcblk0p1

	 Once done jetson board will reboot automatically

-Now connect jetson sbc to monitor using hdmi cable and usb hub to its USB 3.0 port to connect mouse & keyboard and other peripherals. you will be going to experience ubuntu environment in the jetson system.

#####2.2 Kernal installation steps(Follow these steps in jetson board)
#####2.2.1 Download following files

Open the terminal and type following

	$ cd ~
	$ wget http://www.jarzebski.pl/files/jetsontk1/grinch-21.3.4/zImage
 	$ wget http://www.jarzebski.pl/files/jetsontk1/grinch-21.3.4/jetson-tk1-grinch-21.3.4-modules.tar.bz2

#####2.2.2 Check for the avialability of files, to do so follow these instructions in the terminal
	
	$ cd ~
	$ md5sum zImage 
	  a4a4ea10f2fe74fbb6b10eb2a3ad5409  zImage
	$ md5sum jetson-tk1-grinch-21.3.4-modules.tar.bz2 
	  3f84d425a13930af681cc463ad4cf3e6  jetson-tk1-grinch-21.3.4-modules.tar.bz2


#####2.2.3 Now update the kernal
	
	$ cd ~
	$ sudo tar -C /lib/modules -vxjf jetson-tk1-grinch-21.3.4-modules.tar.bz2
	$ sudo apt-get install linux-firmware
	$ sudo cp zImage /boot/zImage
	
	Reboot the system
     
     Default user name : ubuntu
     
     password          : ubuntu
     
      Now check the kernal by connecting turtlebot usb and see whether u can find USB0 (sudo chmod 0777 /dev/ttyUSB0). If so you are successfully finished the  KERNEL installation.


Now jetson board has been configured with ubuntu environment

#####2.3 CUDA Installation

To install CUDA on Jetson TK1 - L4T System
Download cuda kit from the [here](http://developer.download.nvidia.com/embedded/L4T/r21_Release_v3.0/cuda-repo-l4t-r21.3-6-5-prod_6.5-42_armhf.deb)

Execute the following commands in the terminal:

	$ cd /path to cuda package

	$ sudo dpkg -i cuda-repo-<distro>_<version>_<architecture>.deb

	$ sudo apt-get update

	$ sudo apt-get install cuda-toolkit-6-5
