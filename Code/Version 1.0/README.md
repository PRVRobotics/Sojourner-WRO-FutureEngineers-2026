# What can we find in this section of the programing?

In this section, you may find the previous version of our robot’s code and development process.
# Version 1.1
<img width="744" height="520" alt="image_2026-09-11_013150345" src="https://github.com/user-attachments/assets/83470386-463b-4226-826e-8a578d12d785" />


Thinking process of version 1.1
============================================================
Platform: LEGO Spike Prime (Flipper Hub)

Challenge: Open Challenge — Basic Track Navigation

Direction: Counterclockwise

Port Assignments:

   Port C = Drive Motor (main wheels)
   
   Port D = Steering Motor (front wheel angle)

Description:
   This program drives the robot around the track in a
   counterclockwise direction. It uses sequential motor
   commands to drive straight segments and turn corners.
   No sensors are used — the path is pre-programmed based
   on measured track dimensions.

--- WHEN PROGRAM STARTS ---

Step 1: Set motor speeds
motor_C.set_speed(75)        Drive motor at 75% — fast forward speed
motor_D.set_speed(40)        Steering motor at 40% — moderate turn speed

Step 2: Drive forward (first straight segment)
motor_C.run_for(1600, degrees, counterclockwise)
    Drive forward ~1600 degrees of wheel rotation
    Counterclockwise = forward direction for this motor orientation

Step 3: Turn corner — adjust steering left
motor_D.run_for(30, degrees, counterclockwise)
    Turn the steering wheel slightly to prepare for corner

Step 4: Correct steering — bring back to center
motor_C.run_for(150, degrees, clockwise)
    Brief reverse/correction to align through the corner

Step 5: Drive forward (second straight segment)
motor_C.run_for(1200, degrees, counterclockwise)
    Continue driving forward through the next section

Step 6: Straighten steering after turn
motor_D.run_for(30, degrees, clockwise)
    Return steering motor to center position

--- END OF PROGRAM ---

Note: The hub display shows "double it" as a debug message
indicating the program completed successfully.

# Version 1.2
<img width="901" height="580" alt="image_2026-09-11_013457788" src="https://github.com/user-attachments/assets/86df3341-7f61-44a9-b54b-076f3ab64cbd" />


Thinking process of version 1.2
============================================================
Platform: LEGO Spike Prime (Flipper Hub)
Challenge: Open Challenge — Yaw-Assisted Navigation

Port Assignments:
   Port C = Drive Motor (main wheels)
   Port D = Steering Motor (front wheel angle)
   Hub IMU = Yaw angle tracking (built-in)

Description:
   Enhanced version of the open challenge program. This
   program uses two parallel execution stacks:
     Stack 1: Main driving sequence with yaw monitoring
     Stack 2: Steering motor calibration (runs independently)
   The yaw sensor is used to detect when the robot has
   completed a turn (yaw angle exceeds 100 degrees).

=== STACK 1: MAIN DRIVE SEQUENCE ===
--- WHEN PROGRAM STARTS ---

Step 1: Reset orientation reference
hub.motion.reset_yaw()
    Zero out the yaw angle so all turns are measured
    relative to the starting heading

Step 2: Set motor speeds
motor_C.set_speed(75)        Drive motor at 75% — fast forward speed
motor_D.set_speed(40)        Steering motor at 40% — moderate turn speed

Step 3: Drive forward (first straight segment)
motor_C.run_for(1400, degrees, counterclockwise)
    Drive forward ~1400 degrees of wheel rotation

Step 4: Correct heading — brief clockwise adjustment
motor_C.run_for(150, degrees, clockwise)
    Small reverse to fine-tune position after straight

Step 5: Turn corner — steer right
motor_D.run_for(30, degrees, clockwise)
    Adjust steering angle for corner entry

Step 6: Drive through corner
motor_C.run_for(700, degrees, counterclockwise)
    Drive through the turn

Step 7: Counter-steer to straighten out
motor_D.run_for(35, degrees, counterclockwise)
    Adjust steering back toward center

Step 8: Continue forward
motor_C.run_for(200, degrees, counterclockwise)
    Short forward segment after the turn


=== STACK 2: STEERING CALIBRATION (runs in parallel) ===
--- WHEN PROGRAM STARTS ---

Step 1: Set steering to slow calibration speed
motor_D.set_speed(20)        Slow speed for precise centering

Step 2: Reset the degree counter
motor_D.reset_degree_count()
    Zero out the steering motor's position counter
    so all subsequent moves are relative to this "center"

Step 3: Center the steering
motor_D.run_for(40, degrees, counterclockwise)
    Move the steering motor to a known center position
    This compensates for any drift from the previous run


=== ORPHAN BLOCK: YAW-BASED TURN DETECTION ===
(This block exists in the project but is not connected
 to the main stacks — likely used during development/testing)

motor_C.start(counterclockwise)
    Start driving forward continuously
wait_until(hub.motion.get_yaw() > 100)
    Wait until the robot has turned more than 100 degrees
motor_C.stop()
    Stop the drive motor once the turn is complete

--- END OF PROGRAM ---

# Version 1.3
<img width="579" height="561" alt="image_2026-09-11_013619115" src="https://github.com/user-attachments/assets/21a6f3b0-9f23-4373-9075-0097bbdab4fc" />


Thinking process of version 1.3
============================================================
Platform: LEGO Spike Prime (Flipper Hub)
Challenge: Obstacle Challenge — Autonomous Pillar Avoidance

Port Assignments:
   Port A = Color Sensor (pillar color detection)
   Port C = Drive Motor (main wheels)
   Port D = Steering Motor (front wheel angle)
   Port E = Ultrasonic Distance Sensor (obstacle detection)

Color Codes:
   6  = Green (pass the pillar on the RIGHT side)
   9  = Red   (pass the pillar on the LEFT side)
   -1 = No color detected (wall — increase speed, keep going)

Description:
   The most advanced program. It combines continuous distance
   scanning with color-based decision-making to navigate the
   track and avoid randomly placed colored pillars. The robot
   identifies each pillar's color and executes the appropriate
   avoidance maneuver (right for green, left for red).


=== BLOCK 1: STARTUP — INITIAL CALIBRATION ===
--- WHEN PROGRAM STARTS ---

Step 1: Set initial motor speeds
motor_C.set_speed(40)        Drive motor at 40% — moderate approach speed
motor_D.set_speed(25)        Steering motor at 25% — slow, precise turns

Step 2: Center steering
motor_D.run_for(25, degrees, clockwise)
    Nudge steering to a known starting position

Step 3: Initial forward drive
motor_C.run_for(600, degrees, counterclockwise)
    Drive forward toward the first wall or obstacle

Step 4: Steer adjustment
motor_D.run_for(50, degrees, counterclockwise)
    Adjust heading during approach

Step 5: Continue forward
motor_C.run_for(250, degrees, counterclockwise)
    Drive a shorter segment

Step 6: Re-center steering
motor_D.run_for(25, degrees, clockwise)
    Bring steering back to center


=== BLOCK 2: FIRST WALL APPROACH ===
(Runs once — handles the initial wall encounter)

if distance_sensor_E < 18 cm:
    Wall or obstacle detected within 18 cm ahead
    
    Switch to faster speeds for wall handling
    motor_C.set_speed(60)    Increase drive speed to 60%
    motor_D.set_speed(30)    Increase steering speed to 30%
    
    Execute wall-following turn
    motor_C.run_for(1500, degrees, counterclockwise)
        Drive a long segment along the wall
    motor_D.run_for(30, degrees, clockwise)
        Steer right to begin corner turn
    motor_C.run_for(900, degrees, counterclockwise)
        Drive through the corner
    motor_D.run_for(35, degrees, counterclockwise)
        Counter-steer to straighten out after turn


=== BLOCK 3: MAIN LOOP — CONTINUOUS OBSTACLE AVOIDANCE ===

while True:  Forever loop — runs until program is stopped

    if distance_sensor_E < 14 cm:
        *** OBSTACLE DETECTED within 14 cm ***
        
        motor_C.stop()
            Immediately stop the drive motor
        
        --- Check pillar color ---
        
        if color_sensor_A == GREEN (code 6):
            GREEN PILLAR — must pass on the RIGHT side
            
            hub.display.image(arrow_right)
                Display a right-arrow icon on the hub LED matrix
                Matrix pattern: "0090000900909090999000900"
            
            motor_C.stop()
            wait(0.5 seconds)
                Brief pause to stabilize before maneuver
            
            === GREEN AVOIDANCE MANEUVER (pass right) ===
            motor_C.run_for(230, degrees, clockwise)
                Reverse away from the pillar
            motor_D.run_for(30, degrees, clockwise)
                Steer RIGHT to go around the pillar
            motor_C.run_for(300, degrees, counterclockwise)
                Drive forward past the pillar on the right
            motor_D.run_for(60, degrees, counterclockwise)
                Counter-steer LEFT to straighten heading
            motor_C.run_for(150, degrees, counterclockwise)
                Continue forward past the pillar
            motor_D.run_for(35, degrees, clockwise)
                Final steering correction back to center
        
        if color_sensor_A == RED (code 9):
            RED PILLAR — must pass on the LEFT side
            
            hub.display.image(arrow_left)
                Display a left-arrow icon on the hub LED matrix
                Matrix pattern: "0090009990909090090000900"
            
            motor_C.stop()
            wait(0.5 seconds)
                Brief pause to stabilize before maneuver
            
            === RED AVOIDANCE MANEUVER (pass left) ===
            motor_C.run_for(230, degrees, clockwise)
                Reverse away from the pillar
            motor_D.run_for(30, degrees, counterclockwise)
                Steer LEFT to go around the pillar
            motor_C.run_for(300, degrees, counterclockwise)
                Drive forward past the pillar on the left
            motor_D.run_for(60, degrees, clockwise)
                Counter-steer RIGHT to straighten heading
            motor_C.run_for(150, degrees, counterclockwise)
                Continue forward past the pillar
            motor_D.run_for(35, degrees, counterclockwise)
                Final steering correction back to center
        
        if color_sensor_A == NO_COLOR (code -1):
            NO COLOR — this is a wall, not a pillar
            
            motor_C.set_speed(60)
                Increase drive speed for wall-following
            motor_C.start(counterclockwise)
                Start driving forward continuously at high speed
    
    else:
       No obstacle within 14 cm — keep driving
      motor_C.start(counterclockwise)
            Continue driving forward at current speed

--- END OF MAIN LOOP (runs until hub button is pressed) ---
