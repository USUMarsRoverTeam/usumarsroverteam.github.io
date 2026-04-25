---
icon: material/robot-industrial
title: Robotic Arm
---

## Description
- Arm separate from rover body, base attaches to frame.
- Made up of 6 Degrees of Freedom

| Degree of Freedom | Function/Name | Motor Type                      | Level of Functionality    |
|-------------------|---------------|---------------------------------|---------------------------|
| DOF0              | Yaw           | DC Motor Attached to Gearbox    | :warning: Semi-Functional |
| DOF1              | "Shoulder"    | Linear Actuator                 | Works                     |
| DOF2              | "Elbow"       | Linear Actuator                 | Works                     |
| DOF3              | "Wrist Pitch" | Linear Actuator                 | Works                     |
| DOF4              | "Claw Grab"   | Servo (With Custom Top Plate)   | Works                     |
| DOF5              | "Wrist Spin"  | Servo                           | Works (Velocity Controlled)|

- Claw attaches at DOF4
- Controlled by a Pololu 6-Channel Micro Maestro

## Wiring Notes:
Switched to a DB25 connector for easy connections, this connects to both the Maestro control board as well as a voltage stepdown. On the Maestro, to the DB25 yellow wires are signal and white are ground, and the voltage stepdown limits the wire to 12V to not burn out components on the arm. Currently, the Micro Maestro connects to the rover computer through a USB port, though integration with the Teensy is likely.

## Issues
- Integration with arm is currently pain. (Really sorry David)
- Motor box has been replaced multiple times this year, needs analysis.
- Claw is currently plastic, low grip.
- Arm Main Gearbox seems to have issues