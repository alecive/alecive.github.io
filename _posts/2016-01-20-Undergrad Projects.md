---
layout: post
title: Projects for the 2016 Spring Semester
link: 
link-alt: 
category: blog
description: Alessandro Roncone
article: yes

---

{:.no_toc}

* This line will be replaced by the ToC, excluding the "Contents" header
{:toc}

# 6-month projects

## Project A: Improvements on the tictactoe demo

**Supervisors**: Alessandro Roncone, Olivier Mangin

### A1. Perception

 * Code refactoring 
 * Automatic calibration of the board 
 * Automatic calibration of the HSV segmentation of the tiles

### A2. Action

 * Inverse Kinematics instead of recorded (predefined) actions 
 * Automatic calibration of the demo w.r.t. different table heights
 * Improvements on the vacuum gripper part
 * Better speech synthesizer 

## Project B: SnapCircuit

**Supervisors**: Alessandro Roncone, Olivier Mangin

{% include image.html exturl="http://ecx.images-amazon.com/images/I/81sj9QjDChL._SL1500_.jpg" width="width:65%;"  description="SnapCircuit board with some parts." %}

### B1. Perception

 * Automatic Board detection
 * Automatic segmentation of SnapCircuit Parts on the board
 * Automatic recognition of the topology of the board

### B2. Action

 * Inverse Kinematics for high level control of the end-effector
 * Manipulation of the SnapCircuit Parts and their placement on the board

# Senior Projects

## State of the art in robotics

{% include video.html url="//www.youtube.com/embed/zegs0TSFF6A" %}

## Project C: Better perception → _Self modeling_ 

**Supervisor**: Alessandro Roncone

> *...by 2-3 months, infants engage in exploration of their own body as it moves and acts in the environment. They babble and touch their own body, attracted and actively involved in investigating the rich intermodal redundancies, temporal contingencies, and spatial congruence of self-perception.* [Rochat, 1998]

### Expected result

 * Eventually, a publication :)
 * **DEMO C1:** *Kinematic self calibration*: by starting from a known kinematic model, it is possible to compensate for errors by means of visuo-kinematic calibration. E.g:
 * **DEMO C2:** *Kinematic learning*: by starting with as little information as possible, it is possible to compute a reliable enough kinematic model from self-observation and exploration of the consequences of 
 * **DEMO C3:** *Tool use*

### Bibliography

 * J. W. Hart and B. Scassellati (2011). **A Robotic Model of the Ecological Self**. In: *Proceedings of the 11th IEEE/RAS International Conference on Humanoid Robots (Humanoids 2011)*. Bled, Slovenia, October 2011. [[PDF]](http://scazlab.yale.edu/sites/default/files/files/hart-humanoids-11.pdf)
 * M. Hoffmann et al. (2010). **Body Schema in Robotics: A Review**. In: *IEEE Transactions on Autonomous Mental Development*. Vol. 2, No. 4, Dec 2010. [[PDF]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.357.6076&rep=rep1&type=pdf)
 * P. Rochat (1998). **Self-perception and action in infancy**. *Experimental Brain Research*. 1998


## Project D: Better control → _Reaching in clutter_

{% include video.html url="//www.youtube.com/embed/API96d56v3I" %}

### D1. PERCEPTION

   * Development of a perception algorithm (kinect-based) able to detect obstacles close to the robot's arms
   * Development of a suitable avoidance strategy for the robot

### D2. CONTROL
   * 

### Expected result

 * A publication
 * A cool demo

### Bibliography
