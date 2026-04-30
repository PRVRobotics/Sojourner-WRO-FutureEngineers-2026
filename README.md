# Sojourner 🐐 — WRO Future Engineers 2026

## Team Overview

**Team Name:** PRV Robotics  
**Competition:** WRO Future Engineers 2026  
**Platform:** LEGO Spike Prime (Flipper Hub)  
**Programming Environment:** LEGO Spike Prime App (Word Blocks)  
**Connection:** Bluetooth Low Energy (BLE)

---

## Table of Contents

1. [Designed Solution](#designed-solution)
2. [Vehicle Mobility](#vehicle-mobility)
3. [Power System](#power-system)
4. [Sensors](#sensors)
5. [Obstacle Management](#obstacle-management)
6. [Code Structure](#code-structure)
7. [Electromechanical Integration](#electromechanical-integration)
8. [How to Build, Compile, and Upload](#how-to-build-compile-and-upload)
9. [Engineering Journal](#engineering-journal)
10. [Photos](#photos)
11. [Videos](#videos)
12. [Repository Structure](#repository-structure)

---

## Designed Solution

Sojourner is an autonomous self-driving robot built for the WRO Future Engineers competition. The robot must navigate a rectangular track, handle corners, and avoid or interact with colored traffic-sign pillars (red and green) placed along the course. The vehicle uses a differential-drive steering mechanism where one motor (Port C) handles the main drive wheels and a second motor (Port D) controls the steering angle. A distance sensor (Port E) detects walls and obstacles, while a color sensor (Port A) identifies pillar colors to determine the correct avoidance direction.

The design went through multiple iterations. The team initially prototyped with EV3 LEGO components but found that the EV3 motors lacked the precision required for consistent autonomous navigation. After careful evaluation, the team transitioned to the LEGO Spike Prime system, which offered improved motor accuracy, a more compact form factor, and better integration between sensors and the hub. The front wheels were switched to LEGO Spike wheels for tighter maneuverability, while the rear wheels use wider EV3 wheels for improved traction and stability.

The robot operates in three modes corresponding to three separate programs:

- **Sojourner (open 1):** Open challenge — drives a straight course with corner-turning logic. The drive motor runs at high speed (75%) while the steering motor operates at moderate speed (40%). The program executes a sequence of precise motor rotations to navigate the track in a counterclockwise direction, making turns by briefly adjusting the steering motor.

- **Sojourner (open 2):** Open challenge variant — incorporates a yaw sensor reset for orientation tracking and uses a two-stack parallel execution model. One stack handles the main driving sequence (forward motion and corner turns), while a second stack independently manages the initial steering calibration by resetting the degree counter and centering the steering motor.

- **Sojourner beta 3:** Obstacle challenge — the most advanced program. It uses a continuous sensor-polling loop (`forever` block) that reads the distance sensor on Port E and the color sensor on Port A in real time. When a pillar is detected within 14 cm, the robot stops, identifies the pillar color (green = color code 6, red = color code 9), and executes a specific avoidance maneuver based on the color. Green pillars are passed on the right side, while red pillars are passed on the left side. If no obstacle is detected, the robot continues driving forward. An initial approach sequence handles the first wall encounter at 18 cm distance.

---

## Vehicle Mobility

The robot uses a **two-motor differential steering system**:

- **Drive Motor (Port C):** Controls the main drive wheels. This motor provides forward and reverse motion. Typical operating speeds range from 40% to 75% depending on the program phase. The motor uses degree-based rotation commands for precise distance control (e.g., `run_for 1600 degrees` to travel a straight segment, `run_for 150 degrees clockwise` to execute a turn correction).

- **Steering Motor (Port D):** Controls the front wheel steering angle. Small rotations (25–50 degrees) adjust the heading. The steering motor operates at lower speeds (20–40%) for fine control. Before each run, the steering position is calibrated by resetting the degree counter and moving to a known position.

- **Wheel Configuration:** The front wheels are standard LEGO Spike Prime wheels chosen for their compact size and responsive turning radius. The rear wheels are wider EV3-style wheels selected for increased surface contact and traction on the competition mat.

---

## Power System

The robot is powered by the **LEGO Spike Prime rechargeable lithium-ion battery** integrated into the Spike Prime Hub (Flipper). The battery provides 7.4V nominal voltage and powers both the hub processor, all connected motors, and all sensors through the hub's six I/O ports. The battery is recharged via USB-C and provides approximately 4–6 hours of active use on a full charge.

No external batteries or additional power systems are used. The hub manages power distribution automatically across all connected devices.

---

## Sensors

The robot uses two sensors:

- **Ultrasonic Distance Sensor (Port E):** Measures the distance to walls and obstacles in centimeters. The sensor is mounted on the front of the robot facing forward. In the obstacle challenge program, the sensor continuously polls for objects. A detection threshold of 14 cm triggers the obstacle-avoidance routine, while an 18 cm threshold triggers the initial approach sequence. The sensor provides reliable readings in the range of 4–200 cm.

- **Color Sensor (Port A):** Identifies the color of traffic-sign pillars. The sensor is positioned to detect the color of pillars as the robot approaches them. The program checks for three color conditions:
  - **Green (color code 6):** The pillar must be passed on the right — the robot turns clockwise to go around it.
  - **Red (color code 9):** The pillar must be passed on the left — the robot turns counterclockwise to go around it.
  - **No color detected (code -1):** The robot increases speed and continues forward, interpreting this as a wall boundary rather than a pillar.

- **IMU / Yaw Sensor (Built into Hub):** The Spike Prime Hub has a built-in inertial measurement unit. In the `open 2` program, the yaw angle is reset at the start and used to track orientation. A `wait_until yaw > 100` condition is used in one stack to monitor when the robot has completed a sufficient turn.

---

## Obstacle Management

The obstacle challenge program (`Sojourner beta 3`) uses a layered detection and response strategy:

1. **Continuous Scanning:** A `forever` loop runs the distance sensor check on every iteration. While no obstacle is within 14 cm, the drive motor runs continuously in the counterclockwise direction (forward).

2. **Detection:** When the distance sensor reads below 14 cm, the drive motor stops immediately.

3. **Color Identification:** The color sensor on Port A reads the pillar color.

4. **Avoidance Maneuver — Green Pillar:** The robot reverses slightly (230 degrees clockwise on the drive motor), adjusts steering to the right (30 degrees clockwise on the steering motor), drives forward past the pillar (300 degrees counterclockwise), corrects steering back (60 degrees counterclockwise), continues forward (150 degrees), and re-centers steering (35 degrees clockwise).

5. **Avoidance Maneuver — Red Pillar:** The robot executes a mirrored sequence: reverses (230 degrees clockwise), adjusts steering to the left (30 degrees counterclockwise), drives forward (300 degrees counterclockwise), corrects steering back (60 degrees clockwise), continues forward (150 degrees), and re-centers (35 degrees counterclockwise).

6. **Wall Handling:** If the color sensor returns no color (code -1), the robot interprets this as a wall, increases drive speed to 60%, and continues driving forward at full speed.

7. **Initial Approach:** Before the main loop begins, an `if distance < 18 cm` check runs a fast approach sequence at higher speed (drive at 60%, steering at 30%) to position the robot closer to the first wall or obstacle efficiently.

---

## Code Structure

The source code consists of three LEGO Spike Prime `.llsp3` project files, each containing Word Block programs:

### `Sojourner__open_1_.llsp3`
- **Purpose:** Open challenge — basic track navigation (counterclockwise).
- **Structure:** Single execution stack triggered by "When Program Starts."
- **Modules used:** `flippermotor`, `flipperlight`, `flipperevents`.
- **Logic:** Sequential motor commands — set speeds, drive straight segments, turn corners with steering adjustments.
- **Extensions:** Motor control and LED display.

### `Sojourner__open_2_.llsp3`
- **Purpose:** Open challenge — enhanced navigation with yaw tracking.
- **Structure:** Two parallel execution stacks, both triggered by "When Program Starts."
  - **Stack 1:** Main drive sequence with yaw-assisted turns.
  - **Stack 2:** Steering motor calibration (reset degree count, center steering).
- **Modules used:** `flippermotor`, `flipperevents`, `flippermoresensors`, `flippersensors`, `flippermoremotor`.
- **Logic:** Yaw angle monitoring enables orientation-aware turns; steering calibration runs independently in parallel.

### `Sojourner_beta_3.llsp3`
- **Purpose:** Obstacle challenge — full autonomous navigation with obstacle avoidance.
- **Structure:** Three execution blocks:
  1. **Startup sequence:** Initial motor calibration and first approach.
  2. **Conditional approach:** Distance-based first wall handling.
  3. **Main loop (`forever`):** Continuous distance polling, color detection, and avoidance maneuvers.
- **Modules used:** `flippermotor`, `flipperevents`, `flippersensors`, `flipperlight`.
- **Logic:** Event-driven obstacle response within a polling loop; color-based decision branching for green/red/wall handling.

---

## Electromechanical Integration

All motors and sensors connect to the LEGO Spike Prime Hub (Flipper) via standard LEGO Powered Up cables on specific ports:

| Component              | Port | Function                                      |
|------------------------|------|-----------------------------------------------|
| Drive Motor            | C    | Main wheel propulsion (forward/reverse)       |
| Steering Motor         | D    | Front wheel angle control (left/right)        |
| Color Sensor           | A    | Pillar color identification (red/green/none)  |
| Ultrasonic Sensor      | E    | Distance measurement to walls and obstacles   |
| Hub IMU (internal)     | —    | Yaw angle tracking for orientation            |

The hub communicates with the programming environment (LEGO Spike Prime App) via Bluetooth Low Energy. Programs are compiled within the app and downloaded directly to the hub for execution. During operation, no tethered connection is required — the robot runs fully autonomously.

---

## How to Build, Compile, and Upload

### Requirements
- LEGO Spike Prime Hub (Flipper) with firmware updated to the latest version.
- LEGO Spike Prime App (available on Windows, macOS, iPadOS, ChromeOS, Android).
- Bluetooth-enabled device for connecting to the hub.

### Steps

1. **Install the LEGO Spike Prime App** from your platform's app store or from [education.lego.com](https://education.lego.com).

2. **Open a project file:** Launch the app and open any of the three `.llsp3` files from the `src/` directory:
   - `Sojourner__open_1_.llsp3` — Open challenge (counterclockwise)
   - `Sojourner__open_2_.llsp3` — Open challenge (yaw-assisted)
   - `Sojourner_beta_3.llsp3` — Obstacle challenge

3. **Connect the hub:** Turn on the Spike Prime Hub and connect it via Bluetooth in the app. The hub is named "Sojourner🐐" in the Bluetooth device list.

4. **Verify port connections:** Ensure all motors and sensors are connected to the correct ports as specified in the [Electromechanical Integration](#electromechanical-integration) table above.

5. **Download the program:** Click the **Download** button (play icon) in the Spike Prime App. This compiles the Word Block program and transfers it to the hub.

6. **Run the program:** Press the center button on the hub or tap **Run** in the app. The robot will execute the program autonomously.

### Notes
- The programs are saved as Word Blocks (visual block-based programming), not Python. No text-based compilation is required.
- If you do not have access to the LEGO Spike Prime App, refer to the pseudocode translations in the `src/` folder (`pseudocode_*.txt` files) for a readable version of the program logic.
- The `.llsp3` files are ZIP archives containing a `manifest.json` (project metadata), a `scratch.sb3` (block definitions in Scratch JSON format), and supporting assets.

---

## Engineering Journal

### Week 1 (February 2–4, 2026)

**Prototype Development:** The team began by building a prototype model using EV3 LEGO components. A practice robot was completed and initial programs were created to test basic robot movement and system responsiveness.

**Early Programs:** Two functional programs were developed — one to navigate corners and target a pillar on the left side, and another for the right side. A distance sensor was integrated for the first time.

**Hardware Challenge:** Testing revealed that the EV3 motor system lacked the precision needed for reliable autonomous navigation. The team decided to transition to LEGO Spike Prime for its improved efficiency, compact size, and higher motor accuracy.

**Redesign:** The robot was rebuilt using Spike Prime motors and hub. The wheel configuration was updated: Spike Prime wheels on the front for maneuverability, wider EV3 wheels on the back for traction.

**Documentation:** The team created a GitHub account and began planning repository setup. A YouTube account creation was attempted for required competition videos.

---

## Photos

Vehicle photos should be placed in the `v-photos/` directory:
- `front.jpg` — Front view of the vehicle
- `back.jpg` — Back view of the vehicle
- `left.jpg` — Left side view
- `right.jpg` — Right side view
- `top.jpg` — Top-down view
- `bottom.jpg` — Bottom view

Team photo should be placed in the `t-photos/` directory:
- `team.jpg` — Team photo with all members

> **Note:** Photo placeholders are included. Replace with actual photographs before competition submission.

---

## Videos

Competition videos should be uploaded to YouTube and linked here:

- **Open Challenge:** `[YouTube link placeholder — replace with actual URL]`
- **Obstacle Challenge:** `[YouTube link placeholder — replace with actual URL]`

Each video must show at least 30 seconds of autonomous driving on the competition track.

---

## Repository Structure

```
├── README.md                         # This file — full project documentation
├── src/                              # Source code (LEGO Spike Prime project files)
│   ├── Sojourner__open_1_.llsp3      # Open challenge program (counterclockwise)
│   ├── Sojourner__open_2_.llsp3      # Open challenge program (yaw-assisted)
│   ├── Sojourner_beta_3.llsp3        # Obstacle challenge program
│   ├── pseudocode_open_1.txt         # Human-readable pseudocode for open 1
│   ├── pseudocode_open_2.txt         # Human-readable pseudocode for open 2
│   └── pseudocode_beta_3.txt         # Human-readable pseudocode for obstacle challenge
├── models/                           # 3D models or building instructions (if any)
├── schemes/                          # Wiring diagrams and schematics
├── video/                            # Video files or links
├── other/                            # Miscellaneous documentation
├── t-photos/                         # Team photos
└── v-photos/                         # Vehicle photos (all sides, top, bottom)
```

---

## License

This project is shared publicly for the WRO Future Engineers 2026 competition. The repository will remain public for at least 12 months after the competition date.
