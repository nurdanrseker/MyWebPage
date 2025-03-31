---
title: "Implementation Details"
description: "Technical development and problem-solving throughout the VR Horse Riding project."
draft: false
tags: ["implementation", "unity", "quest2", "xr"]
images: ["/images/start.png"]
weight: 4
---

## System Setup and Architecture

The project was developed using **Unity** with the **Meta XR All-In-One SDK**, **XR Interaction Toolkit**, and **XR Plugin Management** system.  

A critical design decision was to position the `OVRCameraRig` on top of a stylized horse prefab’s saddle. This allowed the camera to follow the horse's motion naturally and gave the player a true first-person horse-riding experience.
 ![OVRCameraRig](/images/horse.png)


---

##  Horse Asset Integration

A stylized horse asset from the Unity Asset Store was selected for its visual clarity and animation compatibility.

Steps:
- The correct animated prefab was chosen
- The camera rig was placed and parented to the saddle
- Rigidbody and colliders were configured for grounded movement
- Animator Controller was adjusted for realistic transitions

<iframe width="100%" height="400" 
  src="https://www.youtube.com/embed/cUDdxWHaTEk" 
  title="YouTube video player" frameborder="0" 
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
  allowfullscreen>
</iframe>


---

##  Movement Mechanics

Inspired by real horseback riding, movement was achieved through **controller-based rein gestures**, eliminating the need for joystick or teleportation.

| Action | Gesture |
|--------|---------|
| Move Forward | Hold both grip buttons and move hands up/down |
| Turn | Hold one grip and pull hand outward (left or right) |
| Stop | Hold both grip + trigger buttons and pull both hands backward |


---

## Gesture Processing and Control Logic

All gesture detection was handled in a custom `HorseController.cs` script using:


- `FixedUpdate()` for physics-based detection
- Continuous tracking of controller transforms
- Delta calculations to detect direction and force
- Applying movement via Rigidbody forces and rotation

The inputs were filtered to avoid jitter and ensure smooth transition between motion states.
    ![Check Trigger](/images/checkTrigger.png)

```csharp
public void TurnRight()
{
    m_EulerAngleVelocity = new Vector3(0, 40, 0);
    Quaternion deltaRotation = Quaternion.Euler(m_EulerAngleVelocity * Time.fixedDeltaTime);
        horseRigidbody.MoveRotation(horseRigidbody.rotation * deltaRotation);

    Debug.Log("The horse turns right!");
    StopTurning();
}
```

---

##  Animation Integration and Fixes

The Animator handled three states: **idle**, **walk**, and **stop**. These were triggered via speed thresholds mapped to the horse’s Rigidbody velocity.
 ![Animation](/images/anim.png)


### Problems and Fixes:

- **Sliding during animation**  
   Solution: Enabled `Animate Physics` to match Rigidbody updates  
- **Stutter due to low framerate**  
   Solution: Enabled `Loop Pose`, increased animation FPS  
- **Animator-Rigidbody desync**  
   Solution: Synced state changes using fixed timestep and parameters
   
![Solution](/images/animatePhysics.png)


---

## Motion Optimization

To maintain immersion and reduce discomfort:

- Movement input was smoothed using vector interpolation
- Acceleration and deceleration rates were clamped
- Camera position was synced to mimic subtle horse motion
- Scene had consistent textures and stable horizon line

---

## Final Notes

This project focused on delivering a locomotion experience using intuitive hand gestures, realistic animations, and physical feedback — all without relying on traditional input methods. Through continuous iteration and problem-solving, the system evolved into a fluid and immersive riding mechanic built entirely with accessible Unity tools and open XR components.

