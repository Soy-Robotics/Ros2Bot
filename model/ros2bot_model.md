####ROS2BOT model for your host computer is provided by altering changes for turtlebot description.

Please follow these steps in your host  PC 

  Open the terminal and type following
  
      cd ~/
  
      svn export https://github.com/GaiTech-Robotics/turtlebot/trunk/turtlebot_description
  
  Now copy the turtlebot description and murge it with available turtlebot description in your host PC as well as in Jetson board at (/opt/ros/indigo/share)

####Note: 
To make ros2bot as default model add this line in your bashrc

    export TURTLEBOT_3D_SENSOR=kinect2
