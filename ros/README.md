# Documentations
## 1. [ROS Noetic](https://docs.ros.org/en/noetic/Installation/Ubuntu.html)
## 2. [TurtleBot3](http://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
# Install ROS Noetic
## 1. Update apt
```bash
sudo apt update
```
## 2. Setup sources.list
```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```
## 3. Set up your keys
```bash
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```
## 4. Installation
```bash
sudo apt install ros-noetic-desktop-full
```
# Start with TurtleBot3
## 1. Make workspace
```bash
mkdir -p ~/ws/src
cd ~/ws/src
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
cd ~/ws
catkin_make
```
# SLAM
## 1. Install dependencies
```bash
sudo apt-get install ros-noetic-slam-gmapping
```
## 2. Launch
```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
## 3. Save Map
```bash
sudo apt-get install ros-noetic-map-server
rosrun map_server map_saver -f ~/map
```
# Navigation
## 1. Install dependencies
```bash
sudo apt-get install ros-noetic-navigation
sudo apt-get install ros-noetic-move-base
```
## 2. Launch
```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```
# OpenManipulator X
## 1. Installation
```bash
cd ~/ws/src
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_manipulation.git
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_manipulation_simulations.git
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/open_manipulator_dependencies.git
sudo apt install ros-noetic-ros-control* ros-noetic-control* ros-noetic-moveit*
cd ~/ws
catkin_make
```
## 2. Launch
```bash
roslaunch turtlebot3_manipulation_gazebo turtlebot3_manipulation_world.launch
roslaunch turtlebot3_manipulation_moveit_config move_group.launch
roslaunch turtlebot3_manipulation_moveit_config moveit_rviz.launch config:=true
```
# OpenCR
## 1. Install dependencies
```bash
sudo apt-get install ros-noetic-rosserial-arduino
sudo apt-get install ros-noetic-rosserial
```
## 2. Install OpenCR