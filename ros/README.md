## 1. At the very start
```
sudo apt update
sudo apt upgrade
```
## 2. Install ROS2 Humble -> Follow `https://docs.ros.org/en/humble/Installation.html`
## 3. Initialize ROS2 workspace
```
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
```
## 4. Make ROS executable
```
source /opt/ros/humble/setup.bash
```
## 5. Making a package
```
ros2 pkg create <pkg_name> --build-type ament_python (or ament_cmake) --dependencies rclpy (or rclcpp)
```
## 6. Make package executable
```
cd ~/ros2_ws
source install/setup.bash
```
## 7. Get colcon
```
sudo apt install python3-colcon-common-extensions
```
## 8. Make colcon executable
```
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash
```
## 9. Build package, if you get warnings -> install pip3 and run `pip3 install setuptools==58.2.0`
```
colcon build --symlink-install
```
## 10. Run package
```
ros2 run <pkg_name> <executable_name>
```
## 11. Run package with arguments
```
ros2 run <pkg_name> <executable_name> <arg1> <arg2> ...
```
## 12. Run package with arguments and launch file
```
ros2 launch <pkg_name> <launch_file_name>.launch.py <arg1> <arg2> ...
```
## 13. Run package with arguments and launch file and debug
```
ros2 launch <pkg_name> <launch_file_name>.launch.py <arg1> <arg2> ... --debug
```