---
title: Drivetrain
icon: material/tire
---
## Drive Controllers
The drive controllers are the Spark Max controllers. The best way to troubleshoot the controllers is to use the [producers online light schematic](https://docs.revrobotics.com/brushless/spark-max/status-led) using different color leds to indicate what the type of error is. This LED will also indicate if the specific drive controller has been configured to send a neutral or a breaking signal to the motors. When in the current (6 wheel) configuration the front 2 should receive a breaking signal while the back 4 should be receiving a neutral signal, when they are receiving voltage to the drive controllers. 

### Troubleshooting
If the 3 wires from the drive controllers to the motors(red, black, white) become unplugged, the wire colors should line up correctly. If this is the case and a motor is going in the reverse direction than desired, switching any of the 3 wires should reverse the direction.

Common errors we have encountered with the drive system include disconnection errors, or the signal wire being turned around. We recently created a configuration of the signal and voltage in wires that make them tighter to each other, thus harder to unplug in general. The signal wires should not be high on the potential problem list unless wires have been messed with. The likelier error is disconnection along the encoder wire (rainbow wire from controllers to motors). These have junction points along the extension wires from the drive controllers to the motors. These have been known to become disconnected by vibrations from driving, as well as bumping the wire too hard. If you are seeing an error on a driver, check that these are connected properly before debugging other locations. 

Additionally, the motors will flash their drive state color if the computer/receiver is not on/connected. This is a common indication which is not often a reason to worry, unless everything is on and connected; if this is the case, check the wire from the drive controllers to the Teensy.

### Changing Motor Mode
On the drive controllers, the way to change what mode it defaults to, ie. break or neutral, there is a little red button on the drive controller. This button is adjacent to the status light, and to change the mode, you will need a small pin of some kind the diameter of a paperclip or smaller. You will need to refer to the spark light indicator datasheet to tell what state the controller is in. Purple/magenta should be neutral/freeroll, while blue is representative of brake mode. 

## Motors
- To our knowledge, the motors on the wheels have 2 1:5 gearboxes attached, making it so the RPM is a 1:25 stepdown. This increases torque, but lowers the speed.
- For those less knowledgeable with motors, datasheets have a number that is like XXXXkv, this number represents the RPM of the motor shaft for each volt of input power. Ex. 100kv motor at 12V has an RPM value of 1200 (before any gearbox). For the motors we have on the rover, the maximum voltage is rated for 12V. This is often dictated by either wire limits inside the motor, or integrated encores/electronics.