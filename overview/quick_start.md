---
sort: 3
---

# Quick Start

## WiFi Setup

- Boot the Raspberry Pi. The Raspberry Pi will enter AP mode which will allow you to connect to it over WiFi.

- On a PC, connect to the `Turtlebot4` WiFi network. The password is also `Turtlebot4`.

- Once connected, you can SSH into the Raspberry Pi to configure its WiFi.

```bash
ssh ubuntu@10.42.0.1
```
- The default password is `turtlebot4`

- In the home folder there will be a script called `wifi.sh` which can be used to configure the Raspberry Pi's WiFi:

```bash
bash ~/wifi.sh -s "YOUR_WIFI_SSID" -p "YOUR_WIFI_PASSWORD" -c YOUR_REGULATORY_DOMAIN && sudo reboot
```
Note: The Regulatory domain is based on the country you live in. For a full list, click [here](https://www.arubanetworks.com/techdocs/InstantWenger_Mobile/Advanced/Content/Instant%20User%20Guide%20-%20volumes/Country_Codes_List.htm#regulatory_domain_3737302751_1017918).

- Your Raspberry Pi will reboot and connect to your WiFi network.
- On your PC, run `ros2 topic list` to ensure that the Turtlebot4 is publishing its topics.
- Run `ros2 topic echo /ip` to read the new IP of the Raspberry Pi. On the Turtlebot4 Standard this will also be displayed on the screen.
- You can now SSH into the Turtlebot4 at the new IP and begin using it.

```bash
ssh ubuntu@xxx.xxx.xxx.xxx
```