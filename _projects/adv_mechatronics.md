---
layout: project
title: Android Powered Racer
date: July 5, 2016
image: tcup_front.jpg
---

# Demo

video

# Overview

This project was to design and build a small robot that could follow a line as fast as possible. An android phone was used to power the robot and track the line. A PIC32 controlled the motors. The body and wheels of the robot were 3D printed.

## Android Code

The app used 2 lines of the camera image to find the line. These lines were at 15 and 350 pixels from the top. A Center Of Mass (COM) is calculated for each line, and these values are used to determine the state.

A checkbox called Race Start controlles when data is being sent to the PIC. A stop command is sent anytime data isn’t being sent.

The COM calculation is controlled by 3 sliders that range from 0 - 255, which control the upper red pixel threshold, and the lower blue and green pixel thresholds. The COM’s are also scaled to a range of 0 - 100. 

<img src="/public/images/tcup_back.jpg" alt="Screen View" style="width: 400px;"/>

If the absolute difference between the COMs is less than 110, the the robot is in the “straight line following” state. In this state the first COM values are sent directly to the PIC. The PIC drives both wheels at 100% PWM unless the sent value is outside of the 25 - 75  range. In this case, one wheel is kept at 100% PWM and the other is proportionally controlled based on the sent value. Which wheel is controlled is determined by which side of the range the sent COM is on; < 25 controls the left wheel, > 75 controls the right. This is for minor course corrections while following a relatively straight line or gentle curve. 

If the absolute difference is greater than 110, the the app checks the sign of the difference and which half of the screen the first COM is on. If the first COM is on the left half and the difference is negative, or if it is on the right with a positive difference, then the app is in the “sharp turning’ state. In this state 100 is added to the first COM and this scaled value is sent to the PIC. THe PIC then uses a more aggressive proportional control on one wheel to facilitate steering around a sharper turn. 

If the sign of the difference and the first COM don’t meet the requirements above, then the app is in “line reaquiring” state. This only happens if the robot loses sight of the line, but then finds it again. In this state, 200 is added to the first COM and this value is sent to the PIC. The PIC uses a similarly aggressive proportional control to the “sharp turning” state, but the left and right controls are reversed. 

## Robot Body:
Entire robot designed in OnShape and 3D printed.

Wheels use 3” O-ring and have large elliptical pattern cut-outs to reduce weight and material. The wheels are printed in red ABS plastic.

<img src="/public/images/tcup_iso.jpg" alt="Robot On Line" style="width: 400px;"/>

Body designed to be 2 layered; bottom holds the PIC and H-bridge, top holds phone. The motors are press-fit into protrusions on the side for the front. A small curved extrusion on the back acts as a sliding castor and anchors OTG cable which extends out the back. Holes in the side and front of the body allow access to the ON/OFF switch and PICKit programming pins while PIC is mounted in robot. USER button and LED are accessible from the back opening. A notch in the front ensures unobstructed camera view. The body was printed in grey PLA plastic. 

<img src="/public/images/tcup_biso.jpg" alt="Robot" style="width: 400px;"/>