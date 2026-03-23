---
title: Autonomous
icon: material/brain
---
# Autonomous Documentation

## Simulation

As of 3/22/2026, the autonomous simulation with Gazebo was achieved by very closely following this [playlist](https://www.youtube.com/playlist?list=PLunhqkrRNRhYAffV8JDiFOatQXuU-NnxT)

The entire custom repo that I made can be found at this [link](https://github.com/derekwpinder-arch/dev_ws2)

### Some Notes

- The version of ROS2 and Gazebo used in the video tutorials is NOT the same as is used in my repo. Articulated Robotics uses ROS2 Foxy, while I used ROS2 humble, a newer version.

- The code used to describe the geometry of the robot found in `robot_core` was done by hand, and is currently not an accurate depiction of the rover. I messed around with the [solidworks_urdf_exporter](https://wiki.ros.org/sw_urdf_exporter), but I was running into issues with that I believed was geometry at the time, but may have just been the diff drive steering.

- The plugin `diff_drive` found in `gazebo_control.xacro` doesnt really work... I manually made it so the back 2 wheels do not have any friction, and are colored black. It is my understanding that there used to be a skid_steer plugin back when ROS1 whas being used, but it was removed when everything got upgraded to ROS2. Some work will need to be done to figure it out.
