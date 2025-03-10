---
title:  "3 DoF MeArm Robot"
mathjax: true
layout: post
categories: media
---

<p style="text-align:center;">
    <img width="608" height="478" src="/img/MeArm/MeArm_robot.png" alt="MeArm robot">
</p>

### Overview

[MeArm](https://mearm.com) is a 3 Dof _open source_ robot arm which has various versions. It is considered as a hobby to learn basic concepts of a robotic arm such as, _kinematics_, _embedded hardware_, _programming_ specially C, _control_, _structure and assembly_, and etc. This robot is similar to [Motoman MPK50](https://www.robots.com/robots/motoman-mpk50) which is particularly used for _pick and place_, _packaging_ and _palletizing_ applications, its special structure and morphology make it able to be more _agile_ and _dexterous_ in comparison to typical RRR robots. This case is designed via CAD softwares like __SOLIDWORKS__ and then cut by laser on wooden sheets (MDF). Is includes 4 [plastic gear SG90 servo motors](https://www.tinkermart.in/shop/small-servo-plastic-gear-sg90/), a [Pro Mini 328P Arduino](https://docs.arduino.cc/retired/boards/arduino-pro-mini?queryID=07baba49160a79c79ac8a60ec2d1300c&gl=1*nf7yzt*_ga*MTAzMTY0OTQ0MC4xNjY0MzcxNjg5*_ga_NEXN8H46L5*MTY2NDM3MTY4OS4xLjEuMTY2NDM3MTcxOC4wLjAuMA..)
, a [USB to TTL UART Module](https://www.robofactory.co.za/arduino-modules/158-6pin-cp2102-usb-20-to-ttl-uart-module-6pin-serial-converter.html), a [Breadboard](https://en.wikipedia.org/wiki/Breadboard) and breadboard wires, 5 volt AC DC power supply, and some electornic components. [Joystick Module](https://www.bol.com/nl/nl/p/ps2-joystick-breakout-module-game-controller-voor-arduino-en-raspberry-pi/9300000008325595/?Referrer=ADVNLGOO002013-G-135735704382-S-1678314345586-9300000008325595&gclid=CjwKCAjw4c-ZBhAEEiwAZ105RUMwHQnQxgklasez-0TLup4k1AlCo6KyziLVGZO-M3sZITQ_McglahoC1j0QAvD_BwE) is optional for easier control.

### Project Definition

During `Advanced Robotics` course, as a personal desire, I proposed my [lecturer](https://profile.ut.ac.ir/en/~mudehghani) to implement __Inverse Kinematics__ via _MeArm_. 
1. At first, I had to derive __Forward Kinematics__ of the robot, for this, it is necessary to know (/measure) geometry parameters of _links_, _joints_ and frames, __Denavit-Hartenberg parameters__ ([DH](https://en.wikipedia.org/wiki/Denavit%E2%80%93Hartenberg_parameters)). 
2. Then, set up the controller, structure and connection hardwares to have a reliable and contiuous connection between pc and _MeArm_ (arduino).
3. Next, writing the inverse kinematics _algorithm_ (in C programming language), [USART](https://en.wikipedia.org/wiki/Universal_asynchronous_receiver-transmitter) connection (it is recommended to use standard USART library to read and write data within you code), and _gripper_ program.

<p style="text-align:center;">
    <img width="983" height="576" src="/img/MeArm/hardware_setup.png" alt="set up hardware">
</p>

The goal of the project was deploying the robot to manipulate an object in a structured path, send the initial coordination (defined in Cartesian space in world frame at the center of base vertical joint (x, y, z)) of the end-effector through UART, catch the object, send the desired coordination, finally, send the command to the gripper to release the object. For sending the commands, two micro switches are used; one for action, and the other for the gripper.

<p style="text-align:center;">
    <img width="815" height="616" src="/img/MeArm/Hercules.png" alt="software tool">
</p>

### Challenges

SG90 servo motors do not have any feedback for position and velocity of motors, of course there is an internal closed-loop control system via a potentiometer circuit to dictate the exact position command, so it is not capable for applying position and velocity controllers. <br>
For days I was investigating to find out _torque_ of the motors to calculate __Inverse Dynamics__ for some detection tasks like; applying proper torque to grasp unknown objects. I also did cumbersome trial and error to find __Torque Constants__ of SG90 servos to calculate the torque via current observer, I used a 16-Bit [ADS1115](https://www.adafruit.com/product/1085) ADS module to observe the consumption current for this purpose, while I didn't notice that, it is a 15 &euro; hobby servo motor not a MX-series of _Dynamixel_ servo motors. _SG90_ servos are really inaccurate with a huge _backlash_ and at most 1.8 kg.cm output torque.

### Source Code

The source code is uploaded to [MeArm_robot](https://github.com/Hamid-Manouchehri/MeArm_robot) repository on GitHub. Also the related [video](https://www.linkedin.com/posts/hamid-manouchehri_robotic-mearm-opensource-activity-6857671328384737280-deZS?utm_source=share&utm_medium=member_desktop) post on my LinkedIn illustrates the procedure more. Email me if you have question.
