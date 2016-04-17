---
layout: project
title: Live Video Masking with Gesture Input
date: March 16, 2016
image: motor.jpg
---

# Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/Sj4F_KTDahM" frameborder="0" allowfullscreen></iframe>

# Overview
This project involved using a PIC32 microcontroller and MatLab to control the motion of a DC motor. The final project could be commanded to any angle and could follow a trajectory fairly accuratly. 

<img src="/public/images/annotated_flowchart.jpg" alt="Flowchart of Project" style="width: 400px;"/>

# Trajectories
The trajectories were generated in Matlab and sent to the PIC for the motor to folow. both step and cubic trajectoies were used. After completing the trajectory, the PIC would record the motor's actual trajectory and send it back to MatLab for comparison to the input.

Example trajectory graphs below. The red line is the motor's actual trajectory, and the blue line is the generated trajectory input to the motor.

<img src="/public/images/step.jpg" alt="Example Step trajectory" style="width: 400px;"/>

<img src="/public/images/cubic.jpg" alt="Example Cubic trajectory" style="width: 400px;"/>

# Files

## Github
text
[Here is the Github repo for the project](https://github.com/ncorwin/motor_controller.git)
