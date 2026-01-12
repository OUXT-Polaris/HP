+++
title = ""
date = 2026-01-12T00:00:00
draft = false
share = false
commentable = false
editable = false
+++

## Hulls Design Improvements

### Challenges and Reflections from RoboBoat 2025
At RoboBoat 2025, our team experienced a frustrating result: our ASV capsized during autonomous navigation, preventing us from completing the tasks.
The structural causes were mainly due to the following two points:

*   **High Center of Gravity**: The center of gravity of the entire vessel was too high.
*   **Instability of Hulls Shape**: The "curved high-rocker (banana-shaped)" pontoons we previously used lacked stability on the water surface.

### Drastic Structural Improvements for 2026
To prevent capsizing and ensure mission success, we have implemented the following structural changes for RoboBoat 2026:

*   **Hulls Shape Change (Flat Bottom)**  
    We moved away from the unstable banana shape and newly designed and adopted "flat-bottom" pontoons.
*   **Lower Center of Gravity**  
    We physically lowered the mounting position of the enclosure (waterproof case) housing electronic equipment to reset the center of gravity lower. Additionally, we designed the hulls to house batteries and motor drivers internally, achieving an even lower center of gravity.

<div style="text-align: center; margin: 30px 0;">
  <img src="/img/technical-work/placeholder1.jpg" alt="Hull comparison" style="max-width: 100%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <p style="margin-top: 10px; font-style: italic; color: #666;">Fig 1. The top hull is our new one, and the bottom is the old design. The arrow indicates the cavity that holds the battery box.</p>
</div>

## Other Detailed Design and Implementation

### Ensuring Airtightness and Wiring
We redesigned the wiring path to connect the batteries and motor drivers inside the hull to the external electronics box.
To pass the connectors through while maintaining airtightness, we adopted the following method:

1.  Drilled holes in the hull for wiring.
2.  Used Tupperware (sealed containers) to cover the holes and create an airtight compartment.
3.  Used epoxy resin for bonding to achieve complete waterproofing and airtightness (see Fig 4).

### Securing Connection Strength with the Frame
For connecting the hulls and the frame, we used a method of fixing them with a dedicated jig at one central point on each hull.
However, with a single-point fixation, there was a risk of the jig breaking due to moment loads (twisting and bending forces).
Therefore, we created additional support parts extending from the frame to support both ends of the hulls (see Fig 5). This distributes the load and ensures a stable connection.
The completed design fits within a compact size of less than 1 meter in both length and width.
It can be easily carried by two people, significantly reducing the burden of transport and setup.

<div style="display: flex; flex-wrap: wrap; justify-content: center; gap: 20px; margin-top: 30px;">
  <div style="flex: 1; min-width: 300px; text-align: center;">
    <img src="/img/technical-work/placeholder4.jpg" alt="Wiring and sealing detail" style="max-width: 100%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
    <p style="margin-top: 10px; font-style: italic; color: #666;">Fig 4. Detail of the wiring and sealing using epoxy and tupperware.</p>
  </div>
  <div style="flex: 1; min-width: 300px; text-align: center;">
    <img src="/img/technical-work/placeholder5.jpg" alt="Frame connection support" style="max-width: 100%; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
    <p style="margin-top: 10px; font-style: italic; color: #666;">Fig 5. Additional support structure.</p>
  </div>
</div>


