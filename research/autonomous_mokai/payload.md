# Building an Autonomous Surface Vehicle with the Mokai ES-Kape

## Summary
This guide will overview the process of adding autonomous capabilities to a Mokai ES-Kape using a Pixhawk autopilot and a Linux computer, e.g. an Intel NUC.

This guide will not cover the specifics of partitioning and sealing components. It also attempts to be agnostic to the exact pinouts of the ES-Kape, since Mokai sometimes changes them. This guide is to be used in the process of designing a concrete system; it is not a definition of a concrete system.

## Determining Your ES-Kape Revision
Mokai sometimes changes the electrical configuration of the ES-Kape. The two that the AFRL has worked with will be described here, but this system could work with other configurations as well. Check your ES-Kape with an oscilloscope before building.

The only differences we need to worry about are in the pinouts of the connectors between the main section of the kayak and the engine section.

Photo of engine-section-side connectors:
![engine section side connectors](https://github.com/18r441m/afrl-data/blob/research/research/autonomous_mokai/images/Amphenol7FM.png?raw=true)
Pinouts of Connectors, Looking Head-On

## Summer 2015 Version
### Starboard: Sockets on Bulkhead
![starboard 2015](https://github.com/18r441m/afrl-data/blob/research/research/autonomous_mokai/images/starboard.png?raw=true)

### Port: Pins on Bulkhead
![port 2015](https://github.com/18r441m/afrl-data/blob/research/research/autonomous_mokai/images/bulkhead.png?raw=true)

## Spring 2016 Version
### Starboard: Sockets on Bulkhead
![starboard 2016](https://github.com/18r441m/afrl-data/blob/research/research/autonomous_mokai/images/starboard_2016.png?raw=true)

### Port: Pins on Bulkhead
![port 2016](https://github.com/18r441m/afrl-data/blob/research/research/autonomous_mokai/images/bulkhead_2016.png?raw=true)

## Core System
### Switching
The switching system has four inputs: the two 7-conductor cables from the joystick box and the throttle and steering PWM signals from the Pixhawk. The latter two are easily combined into a single cable, as in the example below. The system also has two outputs: the two cables that will connect to the engine section. The throttle and steering signals from the Pixhawk should be connected into the inputs of a DPDT switch with the throttle and steering signals from the joystick, as shown in the example below. The outputs from the switch should be connected to the output lines as needed by your ES-Kape's pinouts.



![switchbox](https://github.com/18r441m/afrl-data/blob/research/research/autonomous_mokai/images/SwitchBox2.2.png?raw=true)

### Power
At its most basic, the power system simply needs to mediate between the ES-Kape battery—used as a backup for the system—and the main system battery. There are many ways to implement a backup battery. The AFRL used the system shown below because it provides a smooth transition from the main battery to the backup battery, and it slowly charges the backup battery when it has lower voltage than the main battery. Note that if you use a similar system, the resistances and diode forward voltages will need to be calibrated to your expected load.

![backup battery circuit](https://github.com/18r441m/afrl-data/blob/research/research/autonomous_mokai/images/BackupBatteryCircuit2.1.png?raw=true)

## Pixhawk Computer
The computer simply has to be connected over USB to the Pixhawk, with some software to operate on MavLink. For ROS, this means the mavlink package.

## Additional Systems
MavLink over Radio
Direct Remote Control
Secondary GPS
Software Start & Kill
Echo Sounder for Pixhawk
Additional Sensors