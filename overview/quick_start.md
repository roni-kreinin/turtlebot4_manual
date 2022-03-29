---
sort: 3
---

# Quick Start

## WiFi Setup

- Power on the robot by placing it on its dock.

- The Raspberry Pi will boot after a few moments. 

- On the first boot, the Raspberry Pi will enter AP mode which will allow you to connect to it over WiFi.

- On a PC, connect to the `TurtleBot 4` WiFi network. The password is also `TurtleBot 4`.

- Once connected, you can SSH into the Raspberry Pi to configure its WiFi.

```bash
ssh ubuntu@10.42.0.1
```
- The default password is `TurtleBot 4`

- In the home folder there will be a script called `wifi.sh` which can be used to configure the Raspberry Pi's WiFi:

```bash
bash ~/wifi.sh -s "YOUR_WIFI_SSID" -p "YOUR_WIFI_PASSWORD" -c YOUR_REGULATORY_DOMAIN && sudo reboot
```

```note
The Regulatory domain is based on the country you live in. For a full list, click [here](https://www.arubanetworks.com/techdocs/InstantWenger_Mobile/Advanced/Content/Instant%20User%20Guide%20-%20volumes/Country_Codes_List.htm#regulatory_domain_3737302751_1017918).
```

- Your Raspberry Pi will reboot and connect to your WiFi network.
- On your PC, run `ros2 topic list` to ensure that the TurtleBot 4 is publishing its topics.
- Run `ros2 topic echo /ip` to read the new IP of the Raspberry Pi. On the TurtleBot 4 Standard this will also be displayed on the screen.
- You can now SSH into the TurtleBot 4's Raspberry Pi at the new IP and begin using it.

```bash
ssh ubuntu@xxx.xxx.xxx.xxx
```

## Create® 3 WiFi Setup

- Press both Create® 3 button 1 and 2 simultaneously until light ring turns blue
- The Create® 3 is now in AP mode. Connect to its WiFi 'Create-XXXX'
- In a browser go to 192.168.10.1
- Click connect and enter your WiFi ssid and password
- Wait for it to connect to WiFi
- On your PC, run `ros2 topic list` to ensure that the Create® 3 is publishing its topics.

## TurtleBot 4 Controller Setup

- SSH into the TurtleBot 4

```bash
sudo bluetoothctl --agent=NoInputNoOutput
```

- The `bluetoothd` CLI interface will start.
- Type `scan on` and press enter.
- Press and hold both the home and share buttons on the TurtleBot 4 controller until the light starts blinking.
- In the CLI look for a *Wireless Controller* device to be found. It will have a MAC address similar to `A0:5A:5C:DF:4D:7F`.
- Copy the MAC address.
- In the CLI enter `trust MAC_ADDRESS`, replacing `MAC_ADDRESS` with the controllers address.
- Then, enter `pair MAC_ADDRESS`.
- Finally, enter `connect MAC_ADDRESS`.
- The CLI should report that the controller has been connected and the light on the controller will turn blue.
- Enter `exit` to exit the CLI. 