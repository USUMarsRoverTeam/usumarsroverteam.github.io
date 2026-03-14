---
icon: material/hammer-wrench
---
# Starting The Rover

1. Ensure the Rover is connected to the ground station through the ethernet cable and bullets
2. Open Reminna on the ground station
3. **To connect the rover to wifi:**
    1. On the ground station computer navigate to `/home/urc_docker` and run the following:
        ```bash
        ./deimos_nat_setup.sh
        ```
    2. Then through the Remina terminal navigate to `/home/urc_docker` and run the following:
        ```bash
        ./sophia_wifi_setup.sh
        ```
    3. Check the sophia terminal for 3 successful "ping" readings. If you see three successful readings, the rover is now connected to wifi through the ground station computer!
4. **Docker Setup**
    1. Inside the same `urc_docker` folder you can now enter into the docker container for the rover.
    2. On the ground station run the following command:
        ```bash
        ./run_docker_container.sh
        ```
    3. On the rover terminal run the following command:
        ```bash
        ./new_docker_file.sh
        ```
    4. Once inside each docker container verify that you are in the correct ros2 workspace:
        ```bash
        cd
        cd my-rover-workspace
        ```
    5. You can now check that all files are up to date:
        ```bash
        colcon build --symlink-install
        source install/setup.bash
        ```
    6. Now in order to run multiple windows inside the docker we need to open tmux:
        ```bash
        tmux
        source install/setup.bash
        ```
    7. Be sure to source each new window inside of tmux.
5. **Arduino Setup**
    1. To make sure the teensy is properly setup it's helpful to establish the serial communication by flashing the teensy using the Arduino IDE.
    2. Navigate to `/home/Arduino`
    3. Run the executable file for the Arduino IDE. **DO NOT APPLY ANY UPDATES ON THE IDE IF IT ASKS YOU.**
    4. In the `my-rover-workspace` you can open up any of the arduino scripts and flash it to the teensy according to what you are trying to run/do.
    5. Now the rover is ready to be run.
6. **Running the Rover - ROS2 Startup**
    1. On the ground station run the launch file according to what mission you are trying to accomplish. `new_science_module` will be used as an example here:
        ```bash
        ros2 launch rover_bringup new_science_mod_launch.py
        ```
        You can check to see which nodes and topics are up and running:
        ```bash
        ros2 node list
        ros2 topic list
        ros2 topic echo /New_science_module/commands
        ```
    2. On the rover terminal establish the microros serial connection with the teensy:
        ```bash
        ros2 run micro_ros_agent micro_ros_agent serial --dev /dev/ttyACM0
        ```
        Now when you run `ros2 node list` you should see a drive node that wasn't there before. You will also probably need to press the reset button on the teensy to securely establish the connection.

Congratulations, you can now drive and run the rover!
