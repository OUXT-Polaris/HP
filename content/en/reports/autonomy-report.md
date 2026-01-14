+++
title = ""
date = 2026-01-14T00:00:00
draft = false
share = false
commentable = false
editable = false
+++

## **System Configuration and Communication Architecture**

<div style="text-align: center; margin: 30px 0;">
  <img src="/img/technical-work/software_system.png" alt="Software System" style="max-width: 75%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="margin-top: 10px; font-style: italic; color: #666;">Fig 1. Software System</p>
</div>

The Mini-V system is composed of the following elements to achieve both advanced information processing and real-time control.

*   **Hardware Configuration**:<br>We use "NVIDIA Jetson AGX Orin" for the main computer and "Pixhawk" for the flight controller.
*   **Communication Middleware**:<br> We use "ROS 2 (Robot Operating System 2)" as the core of our software development. The system has a modular design, allowing multiple members to develop perception, control, and communication subsystems in parallel.

*   **Communication Automation**:<br> To bridge the communication gap between the high-level computer running ROS 2 (Jetson) and low-level microcontrollers (motor drivers and emergency stop devices), we developed a proprietary mechanism called "ProtoLink".

    *   It automatically generates Protocol Buffer messages from ROS 2 message definitions.
    *   By using nanopb, it generates lightweight C structures compatible with Arduino and STM32 environments, realizing seamless communication without manual protocol maintenance.

<br>

## **Perception System**

<div style="text-align: center; margin: 30px 0;">
  <img src="/img/technical-work/yolo.png" alt="Image inference with YOLO" style="max-width: 75%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="margin-top: 10px; font-style: italic; color: #666;">Fig 2. Image inference with YOLO</p>
</div>

For environment recognition, we use a hybrid sensor fusion combining a camera and LiDAR (Velodyne VLP16). The processing flow is as follows:

1.  **Visual Recognition**:<br> We use "YOLO", capable of high-speed real-time processing, to extract bounding boxes of objects from camera images.
2.  **Point Cloud Processing**:<br> Simultaneously, 3D point cloud data obtained from Velodyne VLP16 is processed using a rule-based algorithm for clustering (classification by chunks).
3.  **Sensor Fusion**:<br> By integrating 2D visual data and 3D point cloud clusters, we identify the "type" and "precise 3D position" of objects.
4.  **Costmap Update**:<br> The integrated obstacle information is sent to Pixhawk and used to update the local costmap for avoidance.

<br>

## **Localization**

Self-position estimation is mainly processed by the "ArduPilot" firmware running on the Pixhawk flight controller.

<div style="text-align: center; margin: 30px 0;">
  <img src="/img/technical-work/pixhawk.png" alt="Pixhawk" style="max-width: 100%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="margin-top: 10px; font-style: italic; color: #666;">Fig 3. Pixhawk</p>
</div>

*   **Sensor Configuration**:<br> GNSS (Global Navigation Satellite System) and IMU (Inertial Measurement Unit) are integrated into Pixhawk, and these data are processed with a Kalman filter to estimate self-position.

*   **Visual Odometry Integration**:<br> In addition to GNSS and IMU data, visual odometry information (movement estimation by image analysis) sent from the ROS 2 main computer is fused to perform self-position estimation and PID control.

<br>

## **Planning & Autonomy**

<div style="text-align: center; margin: 30px 0;">
  <img src="/img/technical-work/mission_planner.png" alt="Simulation with Mission planner" style="max-width: 75%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="margin-top: 10px; font-style: italic; color: #666;">Fig 4. Simulation with Mission planner</p>
</div>



* **Dynamic Path Generation Based on Visual Information**:<br>
  Instead of running on a predetermined route, the route is calculated in real-time from environmental information captured by the camera and LiDAR.

    *   **Identification of Safe Passage Route**: Detects markers on the left and right and calculates their geometric midpoint to identify a safe route to pass through.
    *   **Automatic Waypoint Generation**: Sequentially generates relative waypoints for the calculated target point and steers autonomously to the destination.

<br>

* **Obstacle Detection and Avoidance Function**:<br>
  If there is an obstacle on the navigation route, the robot immediately recognizes it and takes avoidance action.

    *   **Spatial Recognition by Costmap**: Information on recognized obstacles is immediately reflected in the robot's "local costmap" (surrounding map).
    *   **Circumnavigation/Avoidance**: When an obstacle is detected, it identifies the position by verifying with GNSS information, and at the same time performs advanced control to avoid and circumnavigate while keeping a safe distance using LiDAR for distance measurement.

<br>

* **Precision Maneuvering Based on Situational Awareness**:<br>
  It is possible to not only simply move but also understand external signals and dock shapes to perform complex actions.

    *   **Signal Analysis and Action Decision**: Analyzes external signs such as light signals using image recognition, and based on instructions (color or pattern), can navigate to draw complex shapes such as clockwise or counter-clockwise turns.
    *   **High-Precision Approach Control**: In situations where docking to a quay or dock is required, it uses LiDAR ranging data to grasp the distance to the wall surface in units of several centimeters, and accurately approaches and stops at the designated location.

<br>

* **Safety Verification via Simulation**:<br>
  These complex autonomous behaviors are thoroughly verified in a virtual space before operating the actual machine. Through behavior confirmation in a field wider than the actual water surface using SITL (Software-In-The-Loop) environment utilizing Pixhawk and Docker containers, only safe software is deployed to the actual machine.
