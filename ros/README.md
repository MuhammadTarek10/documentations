# Basic ROS2 commands
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