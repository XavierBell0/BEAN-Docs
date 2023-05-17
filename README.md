# BEAN  
## Blimp w/ Efficient Autonomous Navigation

### See build instructions and more specifications at the <a href="https://github.com/XavierBell0/LEAN-Blimp">LEAN-Blimp repo</a>

Small form and long endurance missions require low power robotic systems. Small form factors have limited power sources and therefore can only operate for short periods of time. Long duration missions are more efficient if they consume less power and can function longer. These functions are especially useful for space platforms, monitoring systems, and medicine delivery. Decreasing power consumption increases mission duration. In these small and long duration regimes, the power required for computation and navigation is no longer negligible. 

This repository contains all files necessary to create one of these low power robotic platforms. As part of the MIT LEAN lab, we are pursuing BEAN, a miniature blimp that will use 1 Watt of computation power to 1 Watt of actuation power at 1m/s.

<p align="center">
<img src="https://github.com/XavierBell0/BEAN-Docs/blob/main/READMEimg/BEAN%20closeup.png" height=400px>
  <br>
</p>

#### Table of Contents  
**[Specs](#specs)**<br>
**[Motor Config](#motor-config)**<br>
**[Balloon Choice](#balloon-choice)**<br>
**[Thrust Testing](#thrust-testing)**<br>
**[Electronics](#electronics)**<br>

### Specs
- 7x20mm motors (4)
- 75mm Gemfan HBN props (4)
- L9110s Motor Controller (2)
- INA219 Power Sensor (2)
- MPU6050 IMU (1)
- Raspberry Pi Zero 1.1 W (1)
- 340mAh LiPo battery (2)

Total weight = 79.5g <br>
Balloon max lift = 84.2g
                                                             
### Motor Config
There are many existing motor configurations for blimp-like UAVs in academia and online. These designs were referenced in the creation of BEAN.

<p align="center">
<img src="READMEimg/QuadMotorLayout.jpg" width=400px>
  <br>
  Typical Quad motor layout
</p>
A typical quadcopter has two pairs of motor that rotate in opposite direction with either CW or CCW props. This allows for yaw control by throttling one pair down. Pitch control is acheived by throttling up forward or rear motors. Roll is done by throttling either the right or left side. Linear vertical motion is done through throttling all motors up or down. This suite of four motors gives dynamic and responsive control of the drone in three dimensions. However, this control doesn't translate well to a balloon. To move in the xy plane through pitch and roll, drone convert some of their vertical thrust to some horizontal. However, most of the thrust is still usually contributed to maintaining elevation. In the case of a blimp, the amount of thrust required to move forward and stay afloat is more comparable, so we would have to tilt quite far to get reasonable x/y acceleration. It makes more sense to assign forward motion to dedicated front-facing motors. This allows for most efficient use of thrust.

<br>
<br>

<p align="center" font-size: 10px>
<img src="READMEimg/servo%20control.png" width=600px>
  <br>
   Blimp with (C) Sub-micro Servo SG51R; (D) 8520 Coreless Motor;
</p>
Alvarez presents a lightwieght blimp design in "Evolved Neuromorpic Altitude Controller for an Autonomous Blimp." This design uses two motors and one servo. The motors are coupled to the servo and rotate together. This allows control by tilting the motors in the desired direction. This suite of thrusters gives control similar to a car.

<br>
<br>

<p align="center">
<img src="READMEimg/GTMAB%20motor%20config.png" width=500px>
  <br>
  An example blimp gondola from Georgia Tech with various components located
</p>
The Georgia Tech GT-MAB is designed for "Monocular Vision-based Human Following on Miniature Robotic Blimp." Their condola has five motors: two vertical, two horizontal, and one sideways. This fifth sideways thruster allows for full three dimensional control.

<br>
<br>

<p align="center">
<img src="READMEimg/3%20motor.png" width=500px>
  <br>
  Frame of 3 motor blimp config
</p>
Three motor configurations are somewhat common too, especially in the creation of online hobby projects. These designs use two vertical thrusters and one horizontal or vice versa. While giving the same theoretical control as the two DC motors and one servo setup, the imbalance in angular momentum created by spinning up or down the unpaired thruster will create a torque. This could be fixed by correcting with the other motors, but this is more inefficient. 

<br>
<br>

<p align="center">
<img src="READMEimg/BEANcad.png" width=500px>
  <br>
  BEAN CAD with 4 motors
</p>
BEAN has four thrusters, two horizontal and two vertical. This gives control similar to the servo or 3 motor setup, while avoiding the complexity of the servos and unbalanced torque of 3 motors. Because motors are less efficient at higher current, using two motors to produce some thrust is more efficient than one. The extra motor does add weight, but its within the margins.

<br>
<br>

### Balloon Choice
The main problem with finding a balloon was lack of customizability. Rather than designing the gondola and picking a balloon to fit it, the balloon dictated what  could put on the gondola.

Making a custom envelope would not have been trivial. The material required is hard to purchase online in reasonable quantities and a proper heat seal is vital to operation. Custom making our balloon would also negativily affect repeatibility in future designs.

Finding lift data for balloons is difficult, so we bought standard size party balloon to calibrate testing. The balloon was weighed (no helium), and buoyancy tested. Then the estimated gondola weight as desired lift, found the required diameter for a similarly shaped balloon. The estimated drag on this ideal balloon was calculated to assist in motor selection.

The balloon we chose was the largest one commercially available that has a lift capacity (when filled with >99% helium) of 84.2g. To spend as little power on keeping the blimp airborne as possible, we want our gondola weight to be close to this value. An overall negative buoyancy is desired in case of power failure, otherwise BEAN would just float away.

### Thrust Testing
<p align="center">
  <img src="https://github.com/XavierBell0/BEAN-Docs/blob/main/READMEimg/PropSelection.png" alt="Prop Selection" height="275"/> <img src="https://github.com/XavierBell0/BEAN-Docs/blob/main/READMEimg/testStand.png" alt="Test Stand" height="275" />
  <br>
  Left: Propellers 4-30mm BN, 40mm BN, 55mm BN, 55mm P, 65 HBN OR, 65 HBN Blue, 65mm BN, 75mm HBN, 4in HBN, 5.3in Syma stock <br>
  Right: Thrust test Stand
</p>
  
Thrust testing was performed to determine the most efficient propeller and motor combo. The test stand is shown above. The motor is upside down to keep air from blowing on the scale and disrupting the reading. Once data is  collected into the spreadsheet it can be graphed using the <a href="https://github.com/XavierBell0/LEAN-Blimp/blob/main/testScripts/Thrust%20test%20plotting.py">plotter</a>. Also shown is a reasonable selection of propellers of different shapes and sizes that were used in testing. Dashed lines are testing the same prop on different motors of the same size

<p align="center">
  <img src="https://github.com/XavierBell0/BEAN-Docs/blob/main/READMEimg/PowerVThrust.png" alt="Power V Thrust" height="300"/> <img src="https://github.com/XavierBell0/BEAN-Docs/blob/main/READMEimg/CurrentVEff.png" alt="Current V Efficiency" height="300" />
  <br>
  Full data can be found <a href="https://docs.google.com/spreadsheets/d/1OiYe1rvC_GbhTWiBtDa-APiMod3p-sEL3HPwGkVhBRM/edit#gid=1969339479">here</a>
</p>
BEAN uses 7x20mm motors with 75mm propellers. From the above graphs, one can see that the 75mm propellers are not the most efficient. However, larger propellers require placement further from the center of the gondola. In the event of a crash, the arms could flex and propellers could cut the balloon or damage a surrounding obstacle. By keeping the propellers close, we maintain a key characteristic of soft robots: safe human interaction. The balloon will bump into an obstacle before the propellers do.

While gear driven propellers would increase efficiency, the added weight of gearboxes exceeded our payload limit. Gear driven motors will be vital in future iterations. 

## Electronics
The computer in use is the Raspberry Pi Zero W 1.1. This is connected to an IMU (MPU6050), power sensor (INA219), and 340mAh 1S LiPo. A 5V boost converter steps up the 3.7V input from the battery to power the Pi. Another battery powers the motor controllers (L9110s) and 7x20mm motors. A second power sensor monitors the rate of power consumption. The Pi-side and motor-side circuits are connected through GPIO pins from the controllers to the Pi, I2C from power sensors, and a shared ground. The full schematic can be seen below.

<p align="center">
<img src="READMEimg/BEANSchematic.png" width=500px>
  <br>
  BEAN electrical schematic
</p>

### Initial Electrical Implementation
Wiring was messy on the first interation of BEAN. 2 power sensors, 4 motor controls, 1 IMU, 2 batteries, 1 boost converter, and one Raspberry Pi were all wired according to the above schematic. This resulted in wiring that was hard to debug, visually confusing, and literally heavy. On BEAN, every gram counts.

<p align="center">
<img src="READMEimg/BEANV1Wiring.jpg" width=400px>
  <br>
  BEAN V1 wiring
</p>

### PCB Development
We decided to pursue a custom PCB sheild for the Pi. This PCB would have the following advantages:
- Significant wieght removal
- Remove possible wiring mistakes
- Plugs directly on top of Pi
- Decreases necessary gondola size
- Applicable to any <4 motor robotics projects

And the following system requirements:
- Distributes power from seperate batteries to Pi/sensors and motors respectively
- Deliver stable 5V power from 1S Lipo to Pi
- Collect power data for pi/sensors and motors
- IMU (linear acceleration, rotational rate) data
- Interface with GPIO and I2C pins from Pi
- Control up to 4 motors

As the goal of this PCB was simply to condense the existing configuration, we tried to source from original IC schematics as much as possible. Most of the boards used in BEAN V1 had schematics online that showed component connections and (occasionally) layout were referenced heavily in the creation of the PCB. However, many of these schematics were in provided in EagleCAD while we used Altium. Along with converting syntax, the output pads, headers, and solder jumpers were deleted as these connections would primarily made internal to the PCB. The schematics were then linked using hierarchical design. Then the PCB was generated and the ports (battery, Pi GPIO, motor) placed as desired to guide the layout. Then we carefully placed components around each IC to optimize routing. After components were placed and routed, a power pour was used around the traces to the motor controller. This would avoid noise on the PWM signals generated on these traces. There is also a ground power on the backside of the PCB that can be accessed everywhere with a via. I go into much more detail on PCB development and iteration on these two slide decks <a href="https://docs.google.com/presentation/d/1KbL1qboD9gd7S2Hv6hgaKMFl9PEp3ugSsgFbRh5Mnb4/edit?usp=sharing">PCB V1</a> & <a href="https://docs.google.com/presentation/d/1TrqBSxfiY06AAGJsuXw84zKQXp05J4almzJWHtk7lUM/edit?usp=sharing">PCB V2</a>

<p align="center">
  <img src="READMEimg/PCBLayout.png" alt="Heirachical Design Layout" height="500"/> <img src="READMEimg/PCBV2TopView.png" alt=" " height="500" />
  <br>
  Left: Hierarchical design structure. Note that the power sensing is "downstream" of IMU power so its power draw is not included <br>
  Right: PCB V2 design layout. Power sensors (top), IMU (middle), 5V boost (middle bottom by U6), motor controllers (L shape along bottom)
</p>

This PCB and its corresponding redesigned gondola decreased weight by over 25%. This allowed us to get a smaller more aerodynamiclly stable balloon. However, the gondola is even too light for the balloon as it needs a considerable 8g ballast to reach the desired buoyancy. This gives ample room for the camera and motion capture reflector balls. 

The PCB was also designed for the other LEAN test platforms (a miniature boat and car) and is general purpose for any robotic platform with less than 4 motors.
