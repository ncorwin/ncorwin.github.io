---
layout: project
title: Design of Autonomous Boat Control System
date: April 10, 2015
image: boat.jpg
---

# Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/XpVNH83uMno" frameborder="0" allowfullscreen></iframe>

# Overview
This project was my Senior Design project at Trinity College to complete my BS in Engineering. 

The goal of the project was to design and implement the control system for an autonomous watercraft. This was part of a legacy project at Trinity: Each year, new student teams would work on the overall project. The goal being to be able to compete in the AUVSI Foundation's annual Roboboat competition. 

# Design
The boat was a pontoon-style design with a pair of thrusters under each pontoon. Rudders were designed and attached behind each thruster, and a waterproof housing was designed for the power supply and microcontroller. 

The boat was to navigate by given GPS coordinates, and used an onboard GPS to find a target heading to the given location. It then used an electronic compass to determine it's current heading, and a proportional controller on the rudders to steer towards the target heading. 

## Mechanical
The boat used a pair of Seabotix BT-150 thrusters and was powered by a 12V car battery. 

<img src="/public/images/boat_rudder_cad.png" alt="Solidworks Model of Boat and Rudders" style="width: 400px;"/>

The rudders were designed in Solidworks and 3D printed. They were attached to the boat by adapting the existing structure, and their angle was controlled by waterproof Traxxas 2075 servos.

<img src="/public/images/boat_rudder.jpg" alt="Printed rudders on boat" style="width: 800px;"/>

## Electronics
The rudders, GPS and compass were controlled with an Arduino Uno Microcontroller, and the thrusters were controlled through an H-Bridge.