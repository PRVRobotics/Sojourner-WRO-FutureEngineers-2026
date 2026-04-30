Sojourner 🐐 is WRO Future Engineers 2026

Team Description

The team is called PRV Robotics. It is taking part in the WRO Future Engineers 2026 challenge. The robot runs on a LEGO Spike Prime platform, programmed with the LEGO Spike Prime App (Word Blocks) and connected via Bluetooth.

Solution

Sojourner is an autonomous robot. It drives down the lane, turns corners, and dodges red and green pillars to traverse the field, follow the path, and avoid obstacles as it detects them.

The first prototype was developed with EV3 LEGO components. This gave us an understanding of the robot’s locomotion and how to control its direction with motor power. After testing it for forward and reverse movements, steering to the right and left, and stationary movement, we found the motors to be not precise enough for the project. It was impossible to control the movement distance perfectly and the robot was not capable of turning in the same direction every time.

So we decided to use LEGO Spike Prime parts to develop the final design, due to its better motor precision, quicker response time, smaller dimensions, and ability to connect sensors and control the device easily with a single hub. After that, we redesigned and built the final design.

We also changed the wheels to improve mobility. For smoother movements and control, we used Spike wheels to turn the car in the front wheels and bigger and wider EV3 wheels to keep the wheels grounded to the track in the back wheels.

Mobility

Two motors are used:





Motor 1: drive motor, port C, is used to move the robot forwards and backwards.



Motor 2: steering motor, port D, is used to control the robot’s steering system.

A steering system has been used rather than tank turning. This makes it behave more like a real car and also ensures it can turn more smoothly, providing more control while driving around the corners of the track.

A combination of motor degrees and speed has been used to control the movement. This helps us perform accurate movements consistently. For instance, we use specific values to control forward movements, backward movements, and specific angles for steering movements.

Power

The robot’s power is supplied by the Spike Prime battery installed in the Hub. The battery powers everything on the robot, including the motors, the sensors, and the controller. No external batteries are required.

The robot has plenty of time to run through a test and is charged via USB-C.

Sensors

Two primary sensors are used.





Distance sensor, port E: used to detect walls and any obstacle in front of the robot.



Color sensor, port A: used to detect red and green pillars.

A yaw sensor is also utilized to track direction and improve the robot’s accuracy when turning.

Obstacle Handling

A distance sensor is constantly monitoring the path for any obstacles.

When the robot detects an object nearby, it stops and checks the object with the color sensor.

If the color detected is green, it will turn around the obstacle to the right. If the color detected is red, it will turn around the obstacle to the left. When no color is detected, it will consider it as a wall and move forward.

This pattern repeats for the sequence to turn around the pillar. After the obstacle is cleared, it resumes its journey.

Code Structure

We have developed three distinct programs:





Open 1: This covers simple driving and turning.



Open 2: This program drives the robot using a Yaw sensor for better steering accuracy.



Beta 3: This program handles obstacle avoidance.

The programs were created on Word Blocks, part of the Spike Prime application. Each of the three programs is a standalone unit with its own specific goal and is independently tested. The program for the obstacle avoidance task utilizes a loop. A loop makes the robot work in real-time, checking and responding to sensor values as they change.

Electromechanical Integration

All components are attached directly to the Spike Prime hub and are not connected to any intermediate parts:





Drive Motor connected to Port C on the hub.



Steering Motor connected to Port D on the hub.



Color Sensor connected to Port A on the hub.



Distance Sensor connected to Port E on the hub.

The hub acts as the "brain" of the robot and controls all the parts through sending different signals to both the motors and sensors. Once the program is uploaded onto the hub, the robot works entirely on its own and will not require any more inputs during operation.

How to Build, Compile, and Upload





Open the LEGO Spike Prime app.



Open one of the project files within the app.



Switch on the hub.



Connect your laptop and hub using Bluetooth.



Check to ensure that the motors and sensors are connected to the correct ports.



Click download to download the program to the hub.



Run the program.

No additional programs or files are required because the programs are written through the Spike Prime app itself.

Engineering Journal





Week 1: We built the first prototype using the LEGO EV3 parts and started writing the first program to make the robot move. However, we found that we could not get it to work properly with high accuracy. We then decided to replace all parts with Spike Prime, get different wheels for a different design, and began making the final prototype. In the same week, we also opened our GitHub account.



Week 2: We continued our testing and began working with different experiments and coding to make the robot more accurate in its movements.



Week 3: More tests were completed on the robot to achieve higher accuracy, and we began adding code and other programs to make the robot move much better and more naturally. We also opened a YouTube channel but encountered some issues. The distance sensor is added to the robot during this week.



Week 4: More testing and coding were completed during this time, and we began working on code to control the robot and make turns smoother. We began changing different things in the program to improve the final design.



Week 5: Coding was still done in this week on our robot, and more testing was completed with the different movements.



Week 6: The two programs that were made in this week were to allow the robot to turn corners to the pillars on both the left and right side of the robot.



Week 7: We continued working on coding to make the robot turn properly. At this time, we measured the whole field, and we used that information to help change the final design of the program.



Week 8: Testing the program again with the robot to see how accurate it is and making any changes to make the robot more accurate.



Week 9: More testing and coding was done and began working on making the robot better at detecting pillars and making other small changes on the program to make the final design more accurate.



Week 10: During this week, we were focused more on the written report and documentation and fixing other issues with our GitHub account.

Photos

We are providing pictures of the robot from all angles:





Front



Back



Left



Right



Top



Bottom

We are also providing a picture of the team.

Videos





Open Challenge: (add link)



Obstacle Challenge: (add link)

The above videos contain at least 30 seconds of the robot driving on its own.

Repository Structure





README.md



src/





models/



schemes/



video/



t-photos/



v-photos/

Final Note

This is the full design report for our project. During this 10 weeks, we built the robot from the first prototype to the final version, coding and testing it along the way. We tried many things and discovered our own faults and worked on them to create the best possible program and robot in the end. In the final design, the robot can drive on its own and detect objects, reacting appropriately on its own.



