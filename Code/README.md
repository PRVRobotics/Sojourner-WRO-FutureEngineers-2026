# Code

The code represents what the robot will be commanded to do by code block, that being via the spike coding program, not the spike prime program, just the basic program.

# What does our program do? 

The code was created for the purpose of completing the open course in the right direction. It uses ultrasonic distance sensors to measure distances and stop at the correct positions. The robot then uses pre-programmed actions to move in the correct direction throughout the course. While the code is not yet perfectly functional, it successfully allows the robot to complete a large portion of the course.

# Version 2.1
<img width="446" height="503" alt="image" src="https://github.com/user-attachments/assets/e08c97b0-09ae-45ed-803d-5f5b7f5849ef" />

# Systems Thinking process of version 2.1
This version of the program was developed for Version 1 of our robot. Since this version used larger wheels, we set the directional motor D to operate at 40% speed. The acceleration motor C was set to 75% speed to provide greater precision and control during movement.

The program begins by positioning the wheels in a relatively straight position using directional motor D. The robot is then programmed to move forward for 1,400 degrees using acceleration motor C. After completing this movement, acceleration motor C moves 150 degrees in the opposite direction to adjust the robot’s position. Next, directional motor D turns 30 degrees to the right, followed by acceleration motor C moving the robot forward for an additional 700 degrees. Directional motor D then turns 35 degrees to the left. Finally, acceleration motor C moves the robot forward for another 200 degrees.


# Version 2.2
<img width="335" height="367" alt="image" src="https://github.com/user-attachments/assets/c67ae944-db80-43da-8bb4-32da5e57f5dd" />

# Systems Thinking process of version 2.2
This programming sequence was also used for the original robot design, so it uses the same motor speeds as Program 2.1. The program begins by setting the acceleration motor C to 75% speed and the directional motor D to 40% speed. The robot is then programmed to move forward for 1,600 degrees using the acceleration motor. After completing this movement, the directional motor turns 30 degrees to the left. The acceleration motor then moves 150 degrees in the opposite direction to adjust the robot’s position. Next, the robot moves forward for an additional 1,200 degrees. Finally, the directional motor turns 30 degrees to the right, positioning the wheels for the next movement.

# Version 2.3
<img width="203" height="462" alt="image" src="https://github.com/user-attachments/assets/622cea99-040b-4c86-b420-a6537d349b4c" />

# Systems Thinking process of version 2.3

This version of the program was developed for a more advanced stage of our robot, incorporating ultrasonic distance sensors E and F to detect nearby walls and help the robot navigate the course more accurately. Acceleration motor C controls the robot’s forward and backward movement, while directional motor D controls the steering. The program uses conditional statements to determine the robot’s movements based on the distances detected by the sensors.

The program begins by setting the speeds and initial positions of acceleration motor C and directional motor D. The robot then moves forward while continuously receiving information from ultrasonic distance sensors E and F. When the sensors detect that the robot has reached a specific distance from a wall or obstacle, the program uses this information to determine the appropriate movement. Depending on the sensor readings, acceleration motor C moves the robot forward or backward to adjust its position, while directional motor D turns the wheels in the required direction. After each turn, directional motor D is repositioned to help straighten the wheels before the robot continues moving forward. This process allows the robot to use real-time distance measurements to navigate the course instead of relying only on predetermined movement distances, as our previous programs did.


