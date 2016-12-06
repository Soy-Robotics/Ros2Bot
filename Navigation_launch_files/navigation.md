####ROS2BOT navigation files, added few more launch files to the turtlebot navigation package based on kinect2.

To avail those packages please follow below steps in jetson sbc to get navigation launch files

Open the termial

$ cd ~

$ svn export https://github.com/SawYer-Robotics/turtlebot_apps/trunk/turtlebot_navigation/launch

or
$ git clone https://github.com/SawYer-Robotics/turtlebot_apps/trunk/turtlebot_navigation/launch

Now copy these launch files to /opt/ros/indigo/share/turtlebot_navigation/launch

Navigation launch files depends on kinect2 launch files. To avail them follow steps [here](https://github.com/SawYer-Robotics/Ros2Bot/tree/master/kinect2-launch)

