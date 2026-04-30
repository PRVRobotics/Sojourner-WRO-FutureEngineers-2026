Sojourner 🐐 — WRO Future Engineers 2026
Team Overview

Team Name: PRV Robotics
Competition: WRO Future Engineers 2026
Platform: LEGO Spike Prime
Programming: LEGO Spike Prime App (Word Blocks)
Connection: Bluetooth

Solution

Sojourner is an autonomous robot. It drives down the lane, turns corners, and avoids red and green pillars to move through the field and follow the path correctly.

At the beginning, we built a prototype using EV3 LEGO parts. This helped us understand movement and control. After testing forward, backward, and turning, we found that EV3 motors were not precise enough. The robot could not move the same way every time and was not consistent.

Because of this, we switched to LEGO Spike Prime, which gave us:

Better motor precision
Faster response
Smaller design
Easier connection of sensors and control

After switching, we redesigned and built the final version.

We also improved the wheels:

Spike wheels in the front → better turning
Wide EV3 wheels in the back → better traction and stability
Mobility

The robot uses two motors:

Drive Motor (Port C): moves forward and backward
Steering Motor (Port D): controls direction

We used a steering system instead of tank turning. This makes the robot move more like a real car and gives smoother and more controlled turns.

We use motor degrees and speed to keep movements consistent and accurate.

Power

The robot is powered by the Spike Prime battery inside the hub.
It powers all motors, sensors, and the controller.
No external batteries are used.

Sensors

We use two main sensors:

Distance Sensor (Port E): detects walls and obstacles
Color Sensor (Port A): detects red and green pillars

We also use the yaw sensor to improve turning accuracy and direction.

Obstacle Handling

The robot is always checking for obstacles.

If something is close → robot stops
It checks the color
Green → goes around on the right
Red → goes around on the left
No color → treated as a wall and continues forward

After avoiding the obstacle, the robot continues driving normally.

Code Structure

We created three programs:

Open 1: basic driving and turning
Open 2: uses yaw sensor for better control
Beta 3: full obstacle detection and avoidance

All programs are made using Word Blocks in the Spike Prime app.

The obstacle program uses a loop, which allows the robot to react in real time.

Electromechanical Integration

All parts connect directly to the hub:

Drive Motor → Port C
Steering Motor → Port D
Color Sensor → Port A
Distance Sensor → Port E

The hub acts as the brain and controls everything.

Once the program is uploaded, the robot runs fully on its own.

How to Build, Compile, and Upload
Open the LEGO Spike Prime app
Open a project file
Turn on the hub
Connect using Bluetooth
Check ports are correct
Click download
Run the program

Everything is done inside the Spike Prime app.

Engineering Journal

Week 1:
We built the first prototype using EV3 and started programming. We found it was not precise, so we switched to Spike Prime, changed wheels, and started the final build. We also created the GitHub account.

Week 2:
We continued testing and worked on improving movement accuracy.

Week 3:
We tested more, improved movement, and added new code. We also created a YouTube account but had issues. We added the distance sensor.

Week 4:
We continued testing and coding. We improved turning and control and made changes to improve the robot.

Week 5:
More coding and testing were done to improve movement behavior.

Week 6:
We created programs to turn corners and reach pillars on both sides.

Week 7:
We measured the field and used that to improve the program.

Week 8:
We tested again and made small changes for accuracy.

Week 9:
We improved pillar detection and made small adjustments.

Week 10:
We focused on documentation and report writing and fixed issues with GitHub.

Photos

We include photos of the robot from all sides:

Front
Back
Left
Right
Top
Bottom

We also include a team photo.

Videos
Open Challenge:
Obstacle Challenge: 

Repository Structure
README.md
src/
models/
schemes/
video/
t-photos/
v-photos/
Final Note

This project shows our full process from prototype to final robot.
We tested, found problems, fixed them, and improved step by step.

In the end, the robot can:

Drive on its own
Detect obstacles
Make decisions based on sensors
