---
layout: project
title: Baxter Pick and Place Project
date: December 8, 2015
image: baxter-research-robot_1.jpg
---

## Overview
This was a group project for the ME495 Embedded Systems class at Northwestern. I worked with [Rikki Irwin](http://www.mccormick.northwestern.edu/robotics/meet-students/profiles-2015-2016/irwin-rikki.html), [Matt Cruz](http://www.mccormick.northwestern.edu/robotics/meet-students/profiles-2015-2016/cruz-matthew.html), and [Ayush Sharma](http://www.mccormick.northwestern.edu/robotics/meet-students/profiles-2015-2016/sharma-ayush.html) to develop a program for Rethink Robotic's Baxter robot to let it autonomously detect object on a table, pick them up, and sort them into different containers.

![Working on Baxter](/public/images/baxter_msr.jpg)

## Github
[Here is the Github repo for the project](https://github.com/ncorwin/baxter_pick_and_place.git) The full project writeup is in the README.

## Approach
Our approach to the problem was to detect the position of the objects using AR tags and control Baxter's arm using inverse kinematics to position the gripper over the object. 

Then, using the distance sensor in Baxter's arm we use a simple feedback system to move the gripper to the object. This calculation uses a Cartesian trajectory to hold the orientation of the gripper vertical. 

Once the object is grasped, the arm moves to one of two preset drop off  locations determined by metadata in the object's AR tag. 

## Nathan's Work
Of course, we all contributed to the initial brainstorming and final debugging and refining of the programs, so it isn't completely accurate to attribute specific pieces of code to certain people.

Still, my contribution to this project mostly focused on the fine movement feedback system. I mostly designed the move_to_laser.py node and focused mostly on the arm movement and distance feedback control. 



## Videos
Picking up one block:
<iframe width="854" height="480" src="https://www.youtube.com/embed/wu7xhpNeSyo" frameborder="0" allowfullscreen></iframe>

Picking up 6 blocks in a row:
<iframe width="640" height="360" src="https://www.youtube.com/embed/yLr9ckKPtjg" frameborder="0" allowfullscreen></iframe>