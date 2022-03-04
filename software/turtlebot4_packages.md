---
sort: 2
---

# Turtlebot4 Packages

The Turtlebot4 has 4 main repositories for software: [`turtlebot4`](https://github.com/turtlebot/turtlebot4), [`turtlebot4_robot`](https://github.com/turtlebot/turtlebot4_robot), [`turtlebot4_desktop`](https://github.com/turtlebot/turtlebot4_desktop), and [`turtlebot4_simulator`](https://github.com/turtlebot/turtlebot4_simulator). Each repository is also a [metapackage](http://wiki.ros.org/Metapackages) and contains one or more ROS2 packages.

## Turtlebot4

The `turtlebot4` metapackage contains common packages that are used by both `turtlebot4_robot` and `turtlebot4_simulator`.

### Description

The `turtlebot4_description` package contains the URDF description of the robot and the mesh files for each component.

The description can be published with the `robot_state_publisher`.

### Messages

The `turtlebot4_msgs` package contains the custom messages used on the Turtlebot4:

* [UserButton](https://github.com/turtlebot/turtlebot4/blob/galactic/turtlebot4_msgs/msg/UserButton.msg): User Button states.
* [UserLed](https://github.com/turtlebot/turtlebot4/blob/galactic/turtlebot4_msgs/msg/UserLed.msg): User Led control.
* [UserDisplay](https://github.com/turtlebot/turtlebot4/blob/galactic/turtlebot4_msgs/msg/UserDisplay.msg): User Display data.

The Turtlebot4 can also use all of the messages, actions, and services that the iRobot® Create3® platform supports. See [irobot_create_msgs](https://github.com/iRobotEducation/irobot_create_msgs) for more details.

### Navigation

The `turtlebot4_navigation` packages contains launch and configuration files for using SLAM and navigation on the Turtlebot4.

Launch files:
* [Nav Bringup](): Launches navigation. Allows for launch configurations to use SLAM, Nav2, and localization.
* [SLAM Sync](https://github.com/turtlebot/turtlebot4/blob/galactic/turtlebot4_navigation/launch/slam_sync.launch.py): Launches `slam_toolbox` with online synchronous mapping. Recommended for use on a PC.
* [SLAM Async](https://github.com/turtlebot/turtlebot4/blob/galactic/turtlebot4_navigation/launch/slam_async.launch.py): Launches `slam_toolbox` with online asynchronous mapping. Recommended for use on the Raspberry Pi 4.

Nav Bringup launch configuration options:
- **namespace**: Top-level namespace.
    - default: *None*
- **use_namespace**: Whether to apply a namespace to the navigation stack.
    - options: *true, false*
    - default: *false*
- **slam**: Whether to launch SLAM.
    - options: *off, sync, async*
    - default: *off*
- **localization**: Whether to launch localization.
    - options: *true, false*
    - default: *false*
- **nav2**: Whether to launch Nav2.
    - options: *true, false*
    - default: *false*
- **map**: Full path to map yaml file to load.
    - default: */path/to/turtlebot4_navigation/maps/depot.yaml*
- **use_sim_time**: Use simulation (Gazebo) clock if true.
    - options: *true, false*
    - default: *false*
- **param_file**: Full path to the ROS2 parameters file to use for nav2 and localization nodes.
    - default: */path/to/turtlebot4_navigation/config/nav2.yaml*
- **autostart**: Automatically startup the nav2 stack.
    - options: *true, false*
    - default: *true*
- **use_composition**: Whether to use composed bringup.
    - options: *true, false*
    - default: *true*

Running synchronous SLAM:
```bash
ros2 launch turtlebot4_navigation nav_bringup.launch.py slam:=sync
```

Running asynchronous SLAM with Nav2:
```bash
ros2 launch turtlebot4_navigation nav_bringup.launch.py slam:=async nav2:=true
```

Running Nav2 with localization and existing map:
```bash
ros2 launch turtlebot4_navigation nav_bringup.launch.py localization:=true nav2:=true map:=/path/to/map.yaml
```

### Node

The `turtlebot4_node` package contains the source code for the [rclcpp](https://github.com/ros2/rclcpp) node `turtlebot4_node` that controls the robots HMI as well as other logic. This node is used by both the physical robot and the simulated robot.

Publishers:
- **/hmi/display**: *turtlebot4_msgs/msg/UserDisplay*
    - description: The current information that is to be displayed (Standard model only).
- **/ip**: *std_msgs/msg/String*
    - description: The IP address of the Wi-Fi interface. 

Subscribers:
- **/battery_state**: *sensor_msgs/msg/BatteryState*
    - description: Current battery state of the Create 3.
- **/hmi/buttons**: *turtlebot4_msgs/msg/UserButton*
    - description: Button states of the Turtlebot4 HMI (Standard model only).
- **/hmi/display/message**: *std_msgs/msg/String*
    - description: User topic to print custom message to display (Standard model only).
- **/hmi/led**: *turtlebot4_msgs/msg/UserLed*
    - description: User topic to control User LED 1 and 2 (Standard model only).
- **/interface_buttons**: *irobot_create_msgs/msg/InterfaceButtons*
    - description: Button states of Create 3 buttons.
- **/joy**: *sensor_msgs/msg/Joy*
    - description: Bluetooth controller button states (Standard model only).
- **/wheel_status**: *irobot_create_msgs/msg/WheelStatus*
    - description: Wheel status reported by Create 3.

Service Clients:
- **/e_stop**: *irobot_create_msgs/srv/EStop*
    - description: Enable or disable motor stop.
- **/robot_power**: *irobot_create_msgs/srv/RobotPower*
    - description: Power off the robot.

Action Clients:
- **/dock**: *irobot_create_msgs/action/DockServo*
    - description: Command the robot to dock into its charging station.
- **/wall_follow**: *irobot_create_msgs/action/WallFollow*
    - description: Command the robot to wall follow on left or right side using bump and IR sensors.
- **/undock**: *irobot_create_msgs/action/Undock*
    - description: Command the robot to undock from its charging station.

#### Functions

The node has a set of static functions that can be used either with a button or through the display menu.

Currently, the supported functions are:

- **Dock**: Call the */dock* action.
- **Undock**: Call the */undock* action.
- **Wall Follow Left**: Call the */wall_follow* action with direction `FOLLOW_LEFT` and a duration of 10 seconds.
- **Wall Follow Right**: Call the */wall_follow* action with direction `FOLLOW_RIGHT` and a duration of 10 seconds.
- **Power**: Call the */robot_power* service and power off the robot.
- **EStop**: Call the */e_stop* service and toggle EStop state.

The Turtlebot4 Standard also supports the following menu functions:

- **Scroll Up**: Scroll menu up.
- **Scroll Down**: Scroll menu down.
- **Back**: Exit message screen or return to first menu entry.
- **Select**: Select currently highlighted menu entry.
- **Help**: Print help statement.

#### Configuration

This node can be configured using a parameter *.yaml* file. The default robot parameters can be found [here](https://github.com/turtlebot/turtlebot4_robot/blob/galactic/turtlebot4_bringup/config/turtlebot4.yaml). 

Parameters:

- **wifi.interface**: The Wi-Fi interface being used by the computer. This is used to find the current IP address of the computer.
- **menu.entries**: Set menu entries to be displayed. Each entry must be one of the support [functions](#functions).
- **buttons**: Set the function of Create 3 and HMI buttons.
- **controller**: Set the function of Turtlebot4 Controller buttons.

#### Buttons

The `Buttons` class in `turtlebot4_node` provides functionality to all buttons on the robot. This includes the Create 3 buttons, HMI buttons, and Turtlebot4 Controller buttons.
The node receives button states from the */interface_buttons*, */hmi/buttons*, and */joy* topics.

Each button can be configured to have either a single function when pressed, or two functions by using a short or long press. This is done through [configuration](#configuration).

Supported buttons:

```yaml
buttons:
    create3_1:
    create3_power:
    create3_2:
    hmi_1:
    hmi_2:
    hmi_3:
    hmi_4:

controller:
    a:
    b:
    x:
    y:
    up:
    down:
    left:
    right:
    l1:
    l2:
    l3:
    r1:
    r2:
    r3:
    share:
    options:
    home:
```

##### Example

Lets say we want the Turtlebot4 Standard to have the following button functions:
- Make a short press of Create 3 button 1 toggle EStop.
- Power off robot with 5 second press of Home on the Turtlebot4 Controller.
- Short press of HMI button 1 performs Wall Follow Left, long press of 3 seconds performs Wall Follow Right.

Create a new yaml file:

```bash
cd /home/ubuntu/turtlebot4_ws
touch example.yaml
```

Use your favourite text editor and paste the following into `example.yaml`:
```yaml
turtlebot4_node:
  ros__parameters:
    buttons:  
      create3_1: ["EStop"]
      hmi_1: ["Wall Follow Left", "Wall Follow Right", "3000"]

    controller:
      home: ["Power", "5000"]
```

Launch the robot with your new configuration:

```bash
ros2 launch turtlebot4_bringup standard.launch.py param_file:=/home/ubuntu/turtlebot4_ws/example.yaml
```

The buttons should now behave as described in `example.yaml`.

#### LEDs

The `Leds` class in `turtlebot4_node` controls the states of the HMI LEDs on the Turtlebot4 Standard. It is not used for the Turtlebot4 Lite.

There are 5 status LEDs which are controlled by the node: `POWER`, `MOTOR`, `COMMS`, `WIFI`, and `BATTERY`. There are also 2 user LEDs: `USER_1` and `USER_2` which are controlled by the user via the */hmi/led* topic. The `BATTERY` and `USER_2` LEDs consist of a red and green LED which allows them to be turned on as either green, red, or yellow (red + green). The rest are green only.

Status LEDs:
- **POWER**: Always ON while `turtlebot4_node` is running.
- **MOTOR**: ON when wheels are enabled, OFF when wheels are disabled.
    - Wheel status is reported on the */wheel_status* topic.
- **COMMS**: ON when communication with Create 3 is active. OFF otherwise.
    - Receiving data on the */battery_state* topic implies that communication is active.
- **WIFI**: ON when an IP address can be found for the Wi-Fi interface specified in the [configuration](#configuration).
- **BATTERY**: Colour and pattern will vary based on battery percentage.
    - Battery percentage is received on */battery_state* topic.

User LEDs:

The user LEDs can be set by publishing to the */hmi/led* topic with a [UserLed](https://github.com/turtlebot/turtlebot4/blob/galactic/turtlebot4_msgs/msg/UserLed.msg) message.

UserLed message:

- **led**: Which available LED to use.
    - `uint8 USER_LED_1 = 0`
    - `uint8 USER_LED_2 = 1`
- **color**: Which color to set the LED to.
    - `uint8 COLOR_OFF = 0`
    - `uint8 COLOR_GREEN = 1`
    - `uint8 COLOR_RED = 2`
    - `uint8 COLOR_YELLOW = 3`
- **blink_period**: Blink period in milliseconds.
    - `uint32 ms`
- **duty_cycle**: Percentage of blink period that the LED is ON.
    - `float64 (0.0 to 1.0)`

##### Examples

Set `USER_1` to solid green:

```bash
ros2 topic pub /hmi/led turtlebot4_msgs/msg/UserLed "led: 0
color: 1
blink_period: 1000
duty_cycle: 1.0" --once
```

Set `USER_1` OFF:

```bash
ros2 topic pub /hmi/led turtlebot4_msgs/msg/UserLed "led: 0
color: 0
blink_period: 1000
duty_cycle: 1.0" --once
```

Blink `USER_2` red at 5hz with 50% duty cycle:

```bash
ros2 topic pub /hmi/led turtlebot4_msgs/msg/UserLed "led: 1
color: 2
blink_period: 200
duty_cycle: 0.5" --once
```

## Turtlebot4 Robot

The `turtlebot4_robot` metapackage contains packages that are used by the physical Turtlebot4 robot and are run on the robots Raspberry Pi.

### Base

The `turtlebot4_base` package contains the source code for the [rclcpp](https://github.com/ros2/rclcpp) node `turtlebot4_base_node` which runs on the physical robot. This node interfaces with the GPIO lines of the Raspberry Pi which allows it to read the state of the buttons, as well as write to the LEDs and display.

### Bringup

The `turtlebot4_bringup` package contains the launch and configuration files to run the robots software.

Launch files:
* [Joy Teleop](https://github.com/turtlebot/turtlebot4_robot/blob/galactic/turtlebot4_bringup/launch/joy_teleop.launch.py): Launches nodes to enable the bluetooth controller.
* [OAKD](https://github.com/turtlebot/turtlebot4_robot/blob/galactic/turtlebot4_bringup/launch/oakd.launch.py): Launches the OAK-D nodes.
* [RPLIDAR](https://github.com/turtlebot/turtlebot4_robot/blob/galactic/turtlebot4_bringup/launch/rplidar.launch.py): Launches the RPLIDAR node.
* [Robot](https://github.com/turtlebot/turtlebot4_robot/blob/galactic/turtlebot4_bringup/launch/robot.launch.py): Launches the Turtlebot4 nodes.
* [Lite](https://github.com/turtlebot/turtlebot4_robot/blob/galactic/turtlebot4_bringup/launch/lite.launch.py): Launches the Turtlebot4 Lite.
* [Standard](https://github.com/turtlebot/turtlebot4_robot/blob/galactic/turtlebot4_bringup/launch/standard.launch.py): Launches the Turtlebot4 Standard.

Config files:
* [Turtlebot4 Controller](https://github.com/turtlebot/turtlebot4_robot/blob/galactic/turtlebot4_bringup/config/turtlebot4_controller.config.yaml): Configurations for the Turtlebot4 controller.
* [Turtlebot4](https://github.com/turtlebot/turtlebot4_robot/blob/galactic/turtlebot4_bringup/config/turtlebot4.yaml): Configurations for the `turtlebot4_node` and `turtlebot4_base_node`.

### Diagnostics

The `turtlebot4_diagnostics` packages contains the source code and launch files for the Turtlebot4 diagnostics updater.

### Tests

The `turtlebot4_diagnostics` packages contains the source code for the Turtlebot4 system test scripts.

## Turtlebot4 Desktop

The `turtlebot4_desktop` metapackage contains packages used for visualising and interfacing with the Turtlebot4 from a PC.

### Visualisation

The `turtlebot4_viz` package contains launch files and configurations for viewing the robot in Rviz2, and viewing the diagnostics.

Launch files:
* [View Diagnostics](https://github.com/turtlebot/turtlebot4_desktop/blob/galactic/turtlebot4_viz/launch/view_diagnostics.launch.py): Launches `rqt_robot_monitor` to view diagnostic data.
* [View Model](https://github.com/turtlebot/turtlebot4_desktop/blob/galactic/turtlebot4_viz/launch/view_model.launch.py): Launches `rviz2`. Used to view the model and sensor data.
* [View Robot](https://github.com/turtlebot/turtlebot4_desktop/blob/galactic/turtlebot4_viz/launch/view_robot.launch.py): Launches `rviz2`. Used to view the robot while navigating.

## Turtlebot4 Simulator

The `turtlebot4_simulator` metapackage contains packages used to simulate the Turtlebot4 in Ignition Gazebo.

### Ignition Bringup

The `turtlebot4_ignition_bringup` package contains launch files and configurations to launch Ignition Gazebo.

Launch files:
* [Ignition](https://github.com/turtlebot/turtlebot4_simulator/blob/galactic/turtlebot4_ignition_bringup/launch/ignition.launch.py): Launches Ignition Gazebo and all required nodes to run the simulation.
* [ROS Ignition Bridge](https://github.com/turtlebot/turtlebot4_simulator/blob/galactic/turtlebot4_ignition_bringup/launch/ros_ign_bridge.launch.py): Launches all of the required `ros_ign_bridge` nodes to bridge Ignition topics with ROS topics.
* [Turtlebot4 Nodes](https://github.com/turtlebot/turtlebot4_simulator/blob/galactic/turtlebot4_ignition_bringup/launch/turtlebot4_nodes.launch.py): Launches the `turtlebot4_node` and `turtlebot4_ignition_hmi_node` required to control the HMI plugin and robot behaviour.

Ignition launch configuration options:
- **model**: Which Turtlebot4 model to use.
    - options: *standard, lite*
    - default: *standard*
- **rviz**: Whether to launch rviz.
    - options: *true, false*
    - default: *false*
- **slam**: Whether to launch SLAM.
    - options: *off, sync, async*
    - default: *off*
- **nav2**: Whether to launch Nav2.
    - options: *true, false*
    - default: *false*
- **param_file**: Path to parameter file for `turtlebot4_node`.
    - default: */path/to/turtlebot4_ignition_bringup/config/turtlebot4_node.yaml*
- **world**: Which world to use for simulation.
    - default: *depot*
- **robot_name**: What to name the spawned robot.
    - default: *turtlebot4*

Running the simulator with default settings:
```bash
ros2 launch turtlebot4_ignition_bringup ignition.launch.py
```

Running synchronous SLAM with Nav2:
```bash
ros2 launch turtlebot4_ignition_bringup ignition.launch.py slam:=sync nav2:=true rviz:=true
```

### Ignition GUI Plugins

The `turtlebot4_ignition_gui_plugins` package contains the source code for the Turtlebot4 HMI GUI plugin.

The [Turtlebot4 HMI GUI plugin](https://github.com/turtlebot/turtlebot4_simulator/tree/galactic/turtlebot4_ignition_gui_plugins/Turtlebot4Hmi) is only used for the standard model. The lite model uses the [Create3 HMI GUI plugin](https://github.com/iRobotEducation/create3_sim/tree/main/irobot_create_ignition/irobot_create_ignition_plugins/Create3Hmi).

<figure class="aligncenter">
    <img src="images/turtlebot4_hmi_gui.png" alt="Turtlebot4 HMI GUI" style="width: 35%"/>
    <figcaption>Turtlebot4 HMI GUI plugin</figcaption>
</figure>

### Ignition Toolbox

The `turtlebot4_ignition_toolbox` package contains the source code for the Turtlebot4 HMI node. The Turtlebot4 HMI node acts as a bridge between the `turtlebot4_node` and `ros_ign_bridge` to convert the custom [Turtlebot4 messages](#messages) into standard messages such as `Int32` and `String`.