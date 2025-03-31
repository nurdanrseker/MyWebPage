---
title: "Solution"
description: "Exploring the design process, iterations, and final outcome of the VR Horse Riding project."
draft: false
tags: ["vr", "solution", "design"]
images: ["/images/parkour.png"]
weight: 3
---


To tackle the issues of unnatural and disorienting locomotion in VR, I designed a **horse riding simulation system** that uses hand gestures and rhythm-based control for movement.

### Early Concepts

The initial idea was to mimic **rein-based control**, similar to how riders guide a real horse.  
The goal was to allow users to control **direction and speed** using intuitive hand gestures, captured by Meta Quest 2 controllers.

---

#### Move Forward  
Hold both grip buttons and move hands rhythmically up and down to simulate the rhythm of riding.

![Move Forward](/images/f.png)

---

#### Turn (Left or Right)  
Hold one grip button and pull the respective hand outward to steer the horse in that direction.

![Turn Horse](/images/left.png)
![Turn Horse](/images/right.png)

---

#### Stop  
Hold both grip and trigger buttons, then pull both hands backward to signal the horse to stop.

![Stop Horse](/images/b.png)





---
### Prototyping and Iteration Cycles


The first prototype focused on getting the basic **reins movement** detected. I used Unity’s XR Interaction Toolkit to capture left and right hand positions and applied movement vectors accordingly.


Challenges addressed in this phase:

- Motion jitter was resolved by smoothing input with filtered vectors and fixed timestep adjustments  
- Rein responsiveness was calibrated to prevent abrupt speed changes  
- Physics glitches caused by animations were fixed by enabling **Animate Physics** in Unity  
- Animation stutter was eliminated by activating **Loop Pose** and increasing FPS


Several iterations were tested to improve **comfort** and **responsiveness**.


---

### Final Implementation

The final version includes:

- **Virtual reins** that respond to realistic pulling gestures
- **Speed modulation** through rhythmic hand movement
- **Parkour-style course** with coins
- **Audio** for immersion
- **Custom horse asset** with a mounted rider perspective
-  **Animation system** for walking, idle, and turn states using Unity’s Animator



This creates an **engaging and immersive locomotion** experience, rooted in a natural real-world activity.

