---
layout: project
title: Automated Levitation and Manipulation of Droplets
date: December 9, 2016
image: dod_bath.jpg
---

# Demo
<iframe width="560" height="315" src="https://www.youtube.com/embed/KKmmDffYYdw" frameborder="0" allowfullscreen></iframe>

# Project Overview
Effective control of small liquid volumes drives enabling technology in many important fields that are vital to the well being and advancement of society including medicine, chemistry, and biology; examples include screening for drug efficacy and interaction, ecological and biological contaminants, and gene expression.

<img src="/public/images/dod_side_drops.png" alt="Three droplets being levitated and manipulated using mechanical vibration of a thin fluid layer" style="width: 800px;"/>

This project’s focus is on levitation and manipulation of small liquid droplets using vibration. Vertical vibration of a flat surface will be used to suspend droplets above the surface on a thin layer of air, while horizontal vibrations will move drops across the surface. The work relies on the closely related field of frictional manipulation, and on the laboratory’s unique vibratory platform (PPOD) that is capable of generating arbitrary programmable 6-degree-of-freedom vibration patterns.

<img src="/public/images/dod_top_drops.png" alt="Three droplets being levitated and manipulated using mechanical vibration of a thin fluid layer, top view" style="width: 800px;"/>

Previous students have contributed significant work to this project already. The development of the PPOD and the Droplet On Demand (DOD) generator were both contributions from past
researchers. My focus in this project is primarily to develop a two dimension positioning system for the DOD generator and further development and refinement of the automated droplet testing procedures.

# Component Description
This section overviews the various components of the experimental setup, including pictures and descriptions of code operation and equipment behavior.

## PPOD

<img src="/public/images/dod_ppod.jpg" alt="PPOD" style="width: 800px;"/>

Six degree of freedom vibration table developed to manipulate small planar masses. The device consists of six linear actuators coupled to a rigid plate whose movement is sensed by embedded accelerometers and controlled by a computer.

- Can specify different vibration frequencies for vertical motion, horizontal motion in two directions, and rotations about 3 axis

- Vertical vibrations used to bounce droplets

- Horizontal vibration used to apply horizontal acceleration to droplets

## TestingFile.txt (Windows)
Text file used to set experimental parameters. Each line represents an experiment and can performs certain actions: make a droplet at a specific coordinate, change the PPOD vibration frequencies, take a video on both cameras. Multiple such experiments can be performed in
quick succession automatically. Additionally, these lines can be used to set up more intricate conditions, such as creating multiple droplets at different locations then taking extended, high speed videos of them.

- Each line of the text file represents a single experiment run

- Set up using a predefined parameter string that other programs parce

- Controls behavior of PPOD, DOD gantry and cameras

## AreaFreeRun_TrackCam_TestingFile.cpp (Windows) - SDK Runtime 5.1

<img src="/public/images/dod_overhead_camera.jpg" alt="TrackCam" style="width: 800px;"/>

Program that controls the majority of the timing of the automated droplet testing. This program communicates with the Linux and PPOD computers, as well as the PIC32 and Arduino UNO microcontrollers, reads testing parameters from the text file, and captures the video recorded by the TrackCam (overhead) camera.

- Reads set of testing parameters from a text file called 'TestingFile.txt'

- Initializes serial communication port for PIC32, Arduino Uno, and Winsock (UDP messages)

- Performs Homing cycle on the DOD Gantry and moves it to default position (center of PPOD)

- Initializes frame grabber board properties for later use when opening frame grabber

- Local variables definition

- Check last four characters of argv[1] to ensure a .txt file was provided

- Open text file, count the number of lines in text file (commented lines and testing lines), close text file

- Reopen text file

- Main loop controlling the automated testing
  
  * Read next non-commented line containing set of testing parameters
  
  * Determine if first parameter (IDENTIFIER) is loading a PPOD saved signal (S), or writing PPOD acceleration equations (E)
  
  * Share current testing parameters from GUI over to Linux computer via UDP comm
  
  * Open microEnable frame grabber (TrackCam) with certain properties
  
  * Memory allocation for framebuffer and frame numbers
  
  * Receive UDP datagram from Linux computer saying that it is ready to startcapturing the sequence avi
  
  * Move DOD to specified droplet location
  
  * Send UDP message to PPOD controller for modifying the shaking signals
  
  * Waits for UDP message from PPOD (containing error value) to be below a certain threshold value before continuing
  
  * Sends serial command to PIC to create droplet and generate ExSync triggers
  
  * If Cam_Move is True(1), move DOD out of camera frame
  
  * Receive framebuffer data from microEnable frame grabber and stores into buf[], as well as the current frame number
  
  * Write to avi file using VideoWriter - converts framebuffer data from buf[] into OpenCV Matrix (Mat)
  
  * Release OpenCV VideoWriter
  
  * Close frame grabber and free grabber resources
  
  * If PPOD_RESET is True(1), reset PPOD shaking signals to all {0}
  
  * Determine if there are more lines to be read at the end of text file, or at the end of the file -> update RunFlag
  
  * Send RunFlag to Linux via UDP comm, waits for UDP message receival
  
  * This has been commented out, but can be reinstated if necessary:
  	
	- Send filename to Machine B (MATLAB) on the Linux computer to start the automated video analysis of both .avi files
	
	- Receive datagram back from Machine B (MATLAB) saying it has finished analyzing both .avi files
  
  * RunFlag determines whether there are more lines in text file for testing
  	
	- If RunFlag == 1, restarts recording procedure at top of main loop
	
	- If RunFlag == 0, exits main loop
  
  * Close text file
  
  * Also commented out:
  	
	- Send datagram to Machine B (MATLAB) to tell MATLAB there are no more .avi files for analysis
  
  * Close serial port, Winsock, and UDP sockets