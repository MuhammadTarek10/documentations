# Table of Contents
- [Table of Contents](#table-of-contents)
- [ROS2](#ros2)
- [Basic ROS2 commands](#basic-ros2-commands)
  - [1. At the very start](#1-at-the-very-start)
  - [2. Install ROS2 Humble](#2-install-ros2-humble)
  - [3. Initialize ROS2 workspace](#3-initialize-ros2-workspace)
  - [4. Make ROS executable](#4-make-ros-executable)
  - [5. Making a package](#5-making-a-package)
  - [6. Make package executable](#6-make-package-executable)
  - [7. Get colcon](#7-get-colcon)
  - [8. Make colcon executable](#8-make-colcon-executable)
  - [9. Build package](#9-build-package)
  - [10. Run package](#10-run-package)
  - [11. Run package with arguments](#11-run-package-with-arguments)
  - [12. Run package with arguments and launch file](#12-run-package-with-arguments-and-launch-file)
- [Nodes and Topics](#nodes-and-topics)
  - [Creating Publisher Node](#creating-publisher-node)
  - [Creating Subscriber Node](#creating-subscriber-node)

# ROS2
ROS2 is a framework for robotics. It is a collection of tools, libraries and conventions that aim to simplify the task of creating complex and robust robot behavior across a wide variety of robotic platforms.

ROS2 is a complete rewrite of ROS1. It is not backwards compatible with ROS1. ROS2 is a lot more modular and has a lot more features. It is also a lot more complicated to use.

Here is a list of the most important ROS2 packages:
- rclpy: Python client library
- rcpp: C++ client library
- ros2cli: Command line interface
- sensor_msgs: Standard messages for sensors
- std_msgs: Standard messages
- rosserial: ROS serial communication
- i2c_bridge: I2C bridge
- spi_bridge: SPI bridge
# Basic ROS2 commands
## 1. At the very start
```
sudo apt update
sudo apt upgrade
```
## 2. Install ROS2 Humble
Follow https://docs.ros.org/en/humble/Installation.html
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
## 9. Build package
If you get warnings -> install pip3 and run `pip3 install setuptools==58.2.0`
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

# Nodes and Topics
## Creating Publisher Node
```
import rclpy
from rclpy.node import Node

from std_msgs.msg import String

class MinimalPublisher(Node):

    def __init__(self):
        super().__init__('minimal_publisher')
        self.publisher_ = self.create_publisher(String, 'topic', 10)
        timer_period = 0.5  # seconds
        self.timer = self.create_timer(timer_period, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = String()
        msg.data = 'Hello World: %d' % self.i
        self.publisher_.publish(msg)
        self.get_logger().info('Publishing: "%s"' % msg.data)
        self.i += 1

def main(args=None):
    rclpy.init(args=args)

    minimal_publisher = MinimalPublisher()

    rclpy.spin(minimal_publisher)

    minimal_publisher.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```
## Creating Subscriber Node
```
import rclpy
from rclpy.node import Node

from std_msgs.msg import String

class MinimalSubscriber(Node):

    def __init__(self):
        super().__init__('minimal_subscriber')
        self.subscription = self.create_subscription(
            String,
            'topic',
            self.listener_callback,
            10)
        self.subscription  # prevent unused variable warning

    def listener_callback(self, msg):
        self.get_logger().info('I heard: "%s"' % msg.data)

def main(args=None):
    rclpy.init(args=args)

    minimal_subscriber = MinimalSubscriber()

    rclpy.spin(minimal_subscriber)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_subscriber.destroy_node()
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```