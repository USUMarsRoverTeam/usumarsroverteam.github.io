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

## Issues
- Integration with arm is currently pain. (Really sorry David)
- Motor box has been replaced multiple times this year, needs analysis.
- Claw is currently plastic, low grip.