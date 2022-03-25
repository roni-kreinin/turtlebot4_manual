---
sort: 1
---

# Features

## TurtleBot 4

<figure class="aligncenter">
    <img src="media/standard_render.png" alt="Standard Render" style="width: 90%"/>
    <figcaption>TurtleBot 4</figcaption>
</figure>

The TurtleBot 4 is a ROS2-based mobile robot intended for education and research. The TurtleBot 4 is capable of mapping its surroundings and navigation autonomously, running AI models on its camera

It uses a [Create 3](https://edu.irobot.com/what-we-offer/create3) as the base platform, and builds on it with the TurtleBot 4 shell and User Interface (UI) board. Inside the shell sits a Raspberry Pi 4B, which runs the TurtleBot 4 software.

<figure class="aligncenter">
    <img src="media/turtlebot4_rpi.png" alt="RPI4" style="width: 60%"/>
    <figcaption>Raspberry Pi 4B</figcaption>
</figure>


The UI Board offers status and user LEDs, user buttons, and a 128x64 user display. Additionally, it exposes 4 USB type C ports, as well as additional power ports, and some Raspberry Pi pins for the user.

<figure class="aligncenter">
    <img src="media/turtlebot4_ui.png" alt="UI Board" style="width: 60%"/>
    <figcaption>TurtleBot 4 UI Board</figcaption>
</figure>

On top of the UI board sits a [RPLIDAR A1M8](#rplidar-a1m8) 360 degree lidar, and an [OAK-D-Pro](#oak-d-pro) camera. Above the sensors is the sensor tower, which allows the user to customize their TurtleBot4 with additional sensors or payloads. 

## TurtleBot 4 Lite

<figure class="aligncenter">
    <img src="media/lite_render.png" alt="Lite Render" style="width: 90%"/>
    <figcaption>TurtleBot 4 Lite</figcaption>
</figure>

The TurtleBot 4 Lite is a barebones version of the TurtleBot 4. It has just the necessary components for navigation, mapping, and AI applications. The TurtleBot 4 has the same Raspberry Pi 4B, which sits in the cargo bay of the Create 3, as well as the same RPLIDAR A1M8. The camera on the TurtleBot 4 Lite is the [OAK-D-Lite](#oak-d-lite). Additional sensors and payloads can be attached to the Create 3 faceplate, or placed inside the cargo bay.

## Hardware Specifications

| Feature                  | TurtleBot 4 Lite <img src="media/lite_render.png" alt="Lite Render" width="150" style="vertical-align:middle;"/> | TurtleBot 4 <img src="media/standard_render.png" alt="Standard Render" width="200" style="vertical-align:middle;"/> |
|:-------------------------|:-----------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------|
| Size (L x W x H)         | 342 x 339 x 192 mm                                                                                               | 342 x 339 x 351 mm                                                                                                  |
| Weight                   | 3270 g                                                                                                           | 3945 g                                                                                                              |
| Base platform            | iRobot Create® 3                                                                                                 | iRobot Create® 3                                                                                                    |
| Wheels (Diameter)        | 72 mm                                                                                                            | 72 mm                                                                                                               |
| Ground Clearance         | 4.5 mm                                                                                                           | 4.5mm                                                                                                               |
| On-board Computer        | Raspberry Pi 4B 4GB                                                                                              | Raspberry Pi 4B 4GB                                                                                                 |
| Maximum linear velocity  | 0.31 m/s in safe mode, 0.46 m/s without safe mode                                                                | 0.31 m/s in safe mode, 0.46 m/s without safe mode                                                                   |
| Maximum angular velocity | 1.90 rad/s                                                                                                       | 1.90 rad/s                                                                                                          |
| Maximum payload          | 9 kg                                                                                                             | 9 kg                                                                                                                |
| Operation time           | 2h 30m - 4h depending on load                                                                                    | 2h 30m - 4h depending on load                                                                                       |
| Charging time            | 2h 30m                                                                                                           | 2h 30m                                                                                                              |
| Bluetooth Controller     | -                                                                                                                | TurtleBot 4 Controller                                                                                              |
| Lidar                    | RPLIDAR A1M8                                                                                                     | RPLIDAR A1M8                                                                                                        |
| Camera                   | OAK-D-Lite                                                                                                       | OAK-D-Pro                                                                                                           |
| User Power               | VBAT @ 1.9A <br/> 5V @ Low current <br/> 3.3v @ Low current                                                      | VBAT @ 300 mA <br/> 12V @ TBD mA <br/> 5V @ 500 mA <br/> 3.3v @ 250 mA                                              |
| Expansion ports          | USB 2.0 (Type A) x2 <br/> USB 3.0 (Type A) x2                                                                    | USB 2.0 (Type A) x2 <br/> USB 3.0 (Type A) x1 <br/> USB 3.0 (Type C) x4                                             |
| Programmable LEDs        | Create® 3 Lightring                                                                                              | Create® 3 Lightring <br/> User LED x2                                                                               |
| Status LEDs              | -                                                                                                                | Power LED <br/> Motors LED <br/> WiFi LED <br/> Comms LED <br/> Battery LED                                         |
| Buttons and Switches     | Create® 3 User buttons x2 <br/> Create® 3 Power Button x1                                                        | Create® 3 User buttons x2 <br/> Create® 3 Power Button x1 <br/> User Buttons x4                                     |
| Battery                  | 26 Wh Lithium Ion (14.4V nominal)                                                                                | 26 Wh Lithium Ion (14.4V nominal)                                                                                   |
| Dock                     | Included                                                                                                         | Included                                                                                                            |

## Sensors

### RPLIDAR A1M8

<figure class="aligncenter">
    <img src="media/rplidar_a1m8.png" alt="RPLIDAR" style="width: 90%"/>
    <figcaption>RPLIDAR A1M8</figcaption>
</figure>

The RPLIDAR A1M8 is a 360 degree Laser Range Scanner with a 12m range. It is used to generate a 2D scan of the robots surroundings.
Both the TurtleBot 4 and TurtleBot 4 Lite use this sensor. For more information, click [here](https://www.slamtec.com/en/Lidar/A1).

### OAK-D-Lite

<figure class="aligncenter">
    <img src="media/oak-d-lite.png" alt="OAK-D-Lite" style="width: 90%"/>
    <figcaption>OAK-D-Lite</figcaption>
</figure>

The OAK-D-Lite camera from Luxonis uses a 4K IMX214 colour sensor along with a pair of OV7251 stereo sensors to produce high quality colour and depth images. The on-board Myriad X VPU gives the camera the power to run computer vision applications, object tracking, and run AI models. For more information, visit the Luxonis [documentation](https://docs.luxonis.com/projects/hardware/en/latest/pages/DM9095.html).

### OAK-D-Pro

<figure class="aligncenter">
    <img src="media/oak-d-pro.png" alt="OAK-D-Pro" style="width: 90%"/>
    <figcaption>OAK-D-Pro</figcaption>
</figure>

The OAK-D-Pro offers all of the same features the OAK-D-Lite has, but uses higher resolution OV9282 stereo sensors and adds an IR laser dot projector and an IR illumination LED. This allows the camera to create higher quality depth images, and perform better in low-light environments. For more information, visit the Luxonis [documentation](https://docs.luxonis.com/projects/hardware/en/latest/pages/DM9098pro.html).


