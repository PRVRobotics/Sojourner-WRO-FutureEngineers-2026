Sojourner 🐐 — WRO Future Engineers 2026
Team Overview

Team Name: PRV Robotics
Competition: WRO Future Engineers 2026
Platform: LEGO Spike Prime (Flipper Hub)
Programming Environment: LEGO Spike Prime App (Word Blocks)
Connection: Bluetooth Low Energy (BLE)

Table of Contents
Designed Solution
Vehicle Mobility
Power System
Sensors
Obstacle Management
Code Structure
Electromechanical Integration
How to Build, Compile, and Upload
Engineering Journal
Photos
Videos
Repository Structure
Designed Solution

I built an autonomous robot called Sojourner for the WRO Future Engineers competition. The robot drives on a track, turns corners, and avoids red and green pillars.

At first, I used EV3 LEGO parts, but I found that the motors were not precise enough. Because of this, I switched to LEGO Spike Prime, which gave better accuracy, smaller size, and easier integration. I also improved the wheels by using Spike wheels in the front for better turning and wider EV3 wheels in the back for better traction.

The robot uses two motors: one for driving and one for steering. It also uses a distance sensor to detect walls and obstacles and a color sensor to identify pillar colors. The system is powered by the Spike Prime battery inside the hub, and everything connects directly to it.

The robot has three programs. Two are for the open challenge, where the robot drives and turns corners. One program uses basic movement, and the other uses a yaw sensor to track orientation. The third program is for the obstacle challenge. It constantly checks distance and color. When it detects a pillar, it stops, checks the color, and decides how to go around it. Green pillars are passed on the right, red on the left, and if no color is detected, it continues forward as if it is a wall.

The obstacle program runs in a loop where it keeps scanning the environment. When something is closer than a set distance, it reacts immediately. It uses different movement sequences to go around obstacles and then continues driving.

Vehicle Mobility

I use a two-motor system:

Drive Motor (Port C): Moves the robot forward and backward.
Steering Motor (Port D): Controls the direction of the front wheels.

The front wheels are LEGO Spike wheels for better turning, and the back wheels are wider EV3 wheels for better traction and stability.

Power System

The robot is powered by the LEGO Spike Prime rechargeable battery, which powers the hub, motors, and sensors. No external batteries are used.

Sensors
Distance Sensor (Port E): Detects walls and obstacles.
Color Sensor (Port A): Detects red and green pillars.
Yaw Sensor (built into hub): Tracks orientation for more accurate turns.
Obstacle Management

The robot constantly checks distance and color.

If an object is detected, it stops.
If the pillar is green, it goes around it on the right.
If the pillar is red, it goes around it on the left.
If no color is detected, it treats it as a wall and keeps moving forward.
Code Structure

I created three programs:

Open 1: Basic driving and turning.
Open 2: Driving with yaw sensor for better accuracy.
Beta 3: Full obstacle detection and avoidance.

All programs are created using LEGO Spike Prime Word Blocks and uploaded through Bluetooth.

Electromechanical Integration

All components connect to the Spike Prime hub:

Drive Motor → Port C
Steering Motor → Port D
Color Sensor → Port A
Distance Sensor → Port E

The robot runs autonomously once the program is uploaded.

How to Build, Compile, and Upload
Install the LEGO Spike Prime App.
Open one of the project files.
Connect the hub via Bluetooth.
Make sure all components are connected to the correct ports.
Download the program to the hub.
Run the program.
Engineering Journal
Week 1

I built a prototype using EV3 parts, started programming, and tested movement. I realized the system was not precise enough and switched to Spike Prime. I redesigned the robot, improved the wheels, and started integrating sensors. I also created a GitHub account.

Photos

Vehicle photos should include:

Front
Back
Left
Right
Top
Bottom

A team photo should also be included.

Videos
Open Challenge: (YouTube link)
Obstacle Challenge: (YouTube link)

Each video must show at least 30 seconds of autonomous driving.

Repository Structure
README.md
src/
models/
schemes/
video/
t-photos/
v-photos/
License

This project is shared publicly for the WRO Future Engineers 2026 competition and will remain public for at least 12 months after the event.
