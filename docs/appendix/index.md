---
title: Resources
icon: material/book-open-blank-variant
hide:
    - navigation
---
# Learning ROS2

**ROS2 Overview**

Currently ROS2 is used for all of the comms and controls for the different functioning and moving parts of the rover.

Before trying to understand everything immediately, I would recommend becoming familiar with the basics of:

1. Creating a workspace
2. Creating a Python package
3. Creating a C++ package
4. Creating a subscriber
5. Creating a publisher
6. Linking up some controllers and visualizing the data using `ros2 topic echo`

**Resources**

[YouTube Playlist](https://youtube.com/playlist?list=PLLSegLrePWgJudpPUof4-nVFHGkB62Izy&si=LMfDDdRCFhW-kCXI) - Very helpful for learning ROS2. Covers everything listed above including installation, setup, and practical usage.

**Practical Tips**

Depending on how much you would like to pursue this on your own, you may consider getting an external SSD to boot into Linux using your own laptop.

---

# Docker Information

Currently a Docker container is used to run its own mini computer environment. It bundles all ROS2, Linux, and Python dependencies into one consistent space — helpful for getting consistent results from computer to computer.

**Resources**

[YouTube Series](https://www.youtube.com/playlist?list=PLunhqkrRNRhaqt0UfFxxC_oj7jscss2qe) - Helpful for learning Docker. Note: you may run into issues getting controllers recognized in a new container, but proper permissions on input devices is the key principle.
