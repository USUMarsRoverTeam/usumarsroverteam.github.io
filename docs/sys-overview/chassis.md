---
title: Chassis
icon: material/cube-outline
---
## Frame

### Description
- T-slotted
- [Dimensions]
- Sci-mod/Arm Integration

### Issues
- Integration with arm is currently pain. (Sorry David)

---

## Suspension

### Description
- At this very moment, six-wheel bogie design
- Front: Wheel → Motor Mount → Leg → Bar → Frame
- Back: Wheel → Motor Mount → Leg → CF Rod/Frame
- [Dimensions]
- [Motor Power Needs? (Might be better for electronics)]

### Issues
- Six-wheel design is heavy, bulky, and has pinch points.
- Potential four-wheel design is untested.
- Front right wheel is missing a spacer, currently slides on mount.
- Front bar is off the frame's axis, probable large moment there.

---

## Antenna Mount

### Description
- Antenna mounted near back: Frame → CF Rods → Mount → Antenna
- Antenna has raised mode and lowered mode
- [Dimensions]

### Issues
- Resonance issues, current design unrigid.
- New design is untested.
- Frame mounting brackets need to be analyzed, potential weak point.
- Needs more restraint on forward/backward axis.
- Currently on the right side, centered? Would need to cut CF rods.

## Power System
Input on the stepdowns does not, to my knowledge need any adjustment between battery voltage differences if using a different voltage battery. To adjust the desired output voltage, the little blue box on the stepdown has an adjustable potentiometer in the form of a small 1mm brass screw. To adjust the voltage output of the stepdowns, adjusting this screw should show the voltage output on the display.

For the setup, we were trying for one battery, and calculated that for the competition run time, based solely on drive time, would have enough amperage to last the full length of time. This may be needing recalculating using the wattage of the computers, antenna, and other various components. These we assumed to be negligible as the drive system at speed consumes more power. The reason the current setup has 2 batteries plugged in is a lack of current to the drive controllers/motors. We believe this is due to the thinner gauge wires we used in the initial wiring. A possible solution for this, thus lowering mass by ~1-1.5 kg, is to use a higher gauge wire from the main battery to the drive controllers.

## Other Potential Hardware Topics

Electronics box, Drone installations, Antenna ground station, Testing apparatus.