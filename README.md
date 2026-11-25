# trash-robot

**Trash Talkers** — CMU ECE Robotics Capstone

An autonomous mobile robot that keeps shared indoor spaces like offices, hallways, meeting rooms, and shops free of litter. It carries a standard office trash bin and does two jobs:

- **Comes to you.** Press a desk button or tap the web app, and the robot drives to your desk so you can throw trash away without getting up.
- **Cleans up on its own.** On a schedule, it sweeps the floor, finds trash with a camera, and picks it up with a robotic arm. It skips anything it isn't sure about, so it never throws away someone's belongings.

It works safely around people, runs a full workday on one charge, and keeps camera images on the robot. Staff only need to empty the bin.

## System at a glance

| Subsystem | Key parts |
|---|---|
| Mobility base | 2× DC hub motors, FOC driver, casters |
| Navigation | 2D LiDAR, IMU, cliff/ultrasonic sensors — slam_toolbox, robot_localization, Nav2 |
| Perception | Mast RGB-D + wrist depth camera — detector, 4-class classifier, pickup gate, people tracker |
| Manipulation | 5-DOF Dynamixel arm, fin-ray gripper — MoveIt 2 |
| Bin module | Seat sensor, ToF fill sensor, IR break-beam, optional lid |
| Power & docking | 25.6 V LiFePO4 pack, DC-DC rails, charging dock |
| Compute & comms | Jetson Orin NX, STM32H7, Wi-Fi 6 + BLE |
| User interface | Light bar, display, speaker, BLE desk buttons, web app |
| Safety | E-stops, bumper, safety relay, STM32 watchdog |

## Repository layout

```
trash-robot/
├── docs/        # requirements, design, safety analysis, test plans
├── ros2_ws/     # ROS 2 workspace (Jetson)
│   └── src/     #   one package per subsystem
├── firmware/    # STM32 controller and BLE desk button code
├── models/      # trained perception models + training scripts
├── hardware/    # CAD, schematics, BOM
├── test/        # verification tests
└── tools/       # helper scripts
```

## Getting started

```bash
git clone https://github.com/trash-talkers/trash-robot.git
cd trash-robot
```

## Contributing

`main` is protected. All changes go through a pull request (PR) and need one approval.

### 1. Start from the latest `main`
```bash
git checkout main
git pull
```

### 2. Create a branch for your task
```bash
git checkout -b <subsystem>/<short-task>
```
Example: `nav/keepout-filter`

Branch prefixes: `fw/` `nav/` `percep/` `manip/` `bin/` `power/` `ui/` `safety/` `hw/` `docs/`

### 3. Commit your work
```bash
git add .
git commit -m "Short description of the change"
```

### 4. Push and open a PR
```bash
git push -u origin <subsystem>/<short-task>
```
On GitHub, click **Compare & pull request**, add a reviewer, and link the issue with `Closes #<issue-number>`.

### 5. Merge
Once it's approved, use **Squash and merge** and delete the branch.

### Do not commit
- Secrets (passwords, API keys, webhook URLs)
