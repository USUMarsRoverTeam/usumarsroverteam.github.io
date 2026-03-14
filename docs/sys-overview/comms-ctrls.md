---
title: Comms and Controls
icon: material/antenna
---
# Teensy + MicroRos

## Running the MicroRos 
**(Teensy uses MicroRos to communicate as its own ROS2 Node)**

I basically followed this [video](https://www.youtube.com/watch?v=SV7DeB7kDZs) and it worked perfectly.

### Basic checklist

- Install Arduino on computer
- Insert teensy link on the Arduino interface to load the boards: [LINK](https://www.pjrc.com/teensy/td_download.html)
  - If you have linking issues, uninstall the teensy library from File > Manage Libraries > search teensy, then reinstall it. This rebuilds `platform.txt` to the original code.
- Go to the GitHub page to add the correct teensy microros patch: [LINK](https://github.com/micro-ROS/micro_ros_arduino/blob/jazzy/extras/patching_boards/platform_teensy.txt)
  - Navigate to this location on your computer:
     ```
     ~/.arduino15/packages/teensy/hardware/avr/1.59.0
     ```
  - Copy paste the code from the link into `platform.txt`
  - Be sure to change the version to the correct version, in this case `1.59.0`
- Now you can install the microros workspace and run microros:
  ```bash
  colcon build
  source install/setup.bash
  ros2 run micro_ros_setup create_agent_ws.sh
  ros2 run micro_ros_setup build_agent.sh
  source install/setup.bash
  ros2 run micro_ros_agent micro_ros_agent serial --dev /dev/ttyACM0
  ```

- Now the agent is running and is linked to the serial port with your teensy controller.

### Running the Docker

Each time after you edit the docker file/image you need to rebuild that image:

```bash
docker build -t ros2_jazzy_urc:latest .
./run_ros2_container.sh
```

## TMUX Keybinds

> Tmux sometimes changes up the need for a shift input. If it doesn't work, try adding shift before the special character, e.g. `Ctrl + b + Shift + %`

| Keybind                                | Action                                                 |
| -------------------- | -------------------------- |
| `Ctrl+b %`                        | Split pane vertically             |
| `Ctrl+b "`                        | Split pane horizontally        |
| `Ctrl+b <arrow key>` | Move between panes                     |
| `Ctrl+b x`                        | Kill current pane                      |
| `Ctrl+b o`                        | Cycle through panes                 |
| `Ctrl+b z`                        | Zoom current pane                      |
| `Ctrl+b !`                        | Break pane into new window |

## Build and Run rover_teleop

```bash
# 1. Build
cd ~/sophia_ws
colcon build --packages-select rover_teleop
source install/setup.bash

# 2. Run (in separate terminals/tmux panes)
ros2 run joy joy_node
ros2 run rover_teleop joy_to_twist
ros2 topic echo /joy
ros2 topic echo /cmd_vel
```

## Clear Build Files and Rebuild

Cleans entire workspace:

```bash
rm -rf build/ install/ log/
colcon build
source install/setup.bash
```

## Debugging and Testing

**Test the joystick is sending data:**

```bash
jstest /dev/input/js0
```

**Check if teensy is plugged in:**

```bash
ls -la /dev/ttyACM*
```

**Check if js0 is the Logitech controller:**

```bash
udevadm info -a -n /dev/input/js0 | grep -i "Logitech"
```

**Check ROS2 topic data:**

```bash
# Topic info gives you the message type
ros2 topic info /your_topic_name

# Interface show gives you the data type and structure
ros2 interface show <message_type>
```

## Launch Files

```bash
ros2 launch rover_bringup rover_launch.py
ros2 launch rover_bringup old_science_mod_launch.py
```

> **Important:** If you are mapping two controllers and remapping different nodes, make sure the new topic remapping names match. `cmd_vel` is an example — it was remapped to `drive/cmd_vel` and wasn't working because nothing was publishing to `cmd_vel`.

## Running More Publishers and Subscribers on Microros

To locate the `colcon.meta` file, find your Arduino libraries folder:

- **Windows:** `C:\Users\<YourUsername>\Documents\Arduino\libraries\`
- **macOS:** `/Users/<YourUsername>/Documents/Arduino/libraries/`
- **Linux:** `/home/<YourUsername>/Arduino/libraries/`

> **Tip:** Open Arduino IDE and go to **File > Preferences** — the "Sketchbook location" is the parent folder of your libraries directory.

Then navigate to:

```
micro_ros_arduino → extras → library_generation → colcon.meta
```

> **Important:** Simply editing `colcon.meta` with Notepad or VS Code will not change anything. Because `micro_ros_arduino` is a precompiled library, the `.a` static library files are already baked with default limits (usually 5 publishers/subscribers each). You must rebuild the entire library using `library_generation.sh`.

### Rebuild Process

1. Open `colcon.meta` and change `RMW_UXRCE_MAX_PUBLISHERS` and `RMW_UXRCE_MAX_SUBSCRIPTIONS` to your desired number (e.g. 15 or 20)
2. Use the official micro-ROS Docker image (`microros/micro_ros_static_library_builder`) to run the build script
3. After the script finishes, replace the compiled files in the `src` folder of the library

## Connecting Sophia to Wifi Through SSH

On **Deimos (ground station)**, run these once:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o wlp0s20f3 -j MASQUERADE
sudo iptables -A FORWARD -i wlp0s20f3 -o enp0s31f6 -m state --state RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i enp0s31f6 -o wlp0s20f3 -j ACCEPT
```

On **Sophia**, run these:

```bash
sudo ip route add default via 192.168.1.22
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
```

Test with:

```bash
ping 8.8.8.8
```

> **Note:** The iptables rules on Deimos and the `ip route` on Sophia do not persist after a reboot — you'll need to rerun them each time.

# Autonomous Todo List

- [ ] Centralized GitHub for all system code
- [ ] Finish science mod
  - [ ] Where and how to read sensor data
- [ ] Implement autonomous system
- [ ] Integrate cameras
  - [ ] Realsense
  - [ ] Regular cameras
  - [ ] System viewer to observe camera data
- [ ] LED tower pins and code
- [ ] Document all rover startup, code, ROS2 learning, etc
- [ ] Fix the speed/drive algorithm (currently very slow)