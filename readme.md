## Tested version:

    ROS Noetic running Ubuntu 20.04
    Gazebo11 (embedded in Ubuntu 20.04)
    WSL2 on Windows installed with Ubuntu 20.04 and gazebo11

# Installation (Noetic)
## install ros noetic

  http://wiki.ros.org/noetic/Installation/Ubuntu (follow until Desktop-Full Install)
# install necessary package

sudo apt install ros-noetic-ackermann-msgs sudo apt install ros-noetic-ros-control ros-noetic-ros-controllers sudo apt-get install ros-noetic-teleop-twist-keyboard
## Download the simulation

   mkdir -p ~/catkin_ws/src cd ~/catkin_ws/src git clone https://github.com/tuanluong88/ackermann_vehicle.git

cd ~/catkin_ws rosdep install --from-paths src --ignore-src -r -y catkin_make
## Running
## Launch the car model in gazebo
## Open a terminal
  roslaunch ackermann_vehicle_gazebo ackermann_vehicle.launch
  
## Steering command with ackermann_msgs type
    http://docs.ros.org/en/api/ackermann_msgs/html/msg/AckermannDrive.html
## Open another terminal
    rostopic pub -r 10 /ackermann_cmd ackermann_msgs/AckermannDrive "{steering_angle: 1.0, steering_angle_velocity: 0.0, speed: 1.0, acceleration: 0.0, jerk: 0.0}"
## with
/ackermann_vehicle/ackermann_vehicle_gazebo/scripts$
## Open a terminal and Rrun the following commands:
    ./cmd_vel_to_ackermann_drive.py
    
## The python file will wait for /cmd_vel inputs.
## Open another terminal

    rostopic pub -r 10 /cmd_vel geometry_msgs/Twist '{linear: {x: 0.1, y: 0.0, z: 0.0}, angular: {x: 0.0,y: 0.0,z: 0.2}}'

## or using teleop_twist_keyboard package in ros to control through keyboard rosrun teleop_twist_keyboard teleop_twist_keyboard.py
