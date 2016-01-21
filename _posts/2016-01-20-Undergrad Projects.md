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

**Supervisors**: *Alessandro Roncone, Olivier Mangin*

### Task A1. Perception

 * Code refactoring 
 * Automatic calibration of the board 
 * Automatic calibration of the HSV segmentation of the tiles

### Task A2. Action

 * Inverse Kinematics instead of recorded (predefined) actions 
 * Automatic calibration of the demo w.r.t. different table heights
 * Improvements on the vacuum gripper part
 * Better speech synthesizer 

## Project B: SnapCircuit

**Supervisors**: *Alessandro Roncone, Olivier Mangin*

{% include image.html exturl="http://ecx.images-amazon.com/images/I/81sj9QjDChL._SL1500_.jpg" width="width:65%;"  description="SnapCircuit board with some parts." %}

### Task B1. Perception

 * Automatic Board detection
 * Automatic segmentation of SnapCircuit Parts on the board
 * Automatic recognition of the topology of the board

### Task B2. Action

 * Inverse Kinematics for high level control of the end-effector
 * Manipulation of the SnapCircuit Parts and their placement on the board

# Senior Projects

## State of the art in body representation and control

{% include video.html url="//www.youtube.com/embed/zegs0TSFF6A" %}

## Project C: Better perception → _Self modeling_ 

**Supervisor**: *Alessandro Roncone*

> *...by 2-3 months, infants engage in exploration of their own body as it moves and acts in the environment. They babble and touch their own body, attracted and actively involved in investigating the rich intermodal redundancies, temporal contingencies, and spatial congruence of self-perception.* [Rochat, 1998]

### PROJECT C1. Kinematic Learning

By starting with as little information as possible, it is possible to compute a reliable enough kinematic model from self-observation and exploration of the consequences of the robot's actions. See Hart and Scassellati [2011].

### PROJECT C2. Tool Use and object affordances

See Tikhanoff et al [2013], Hart and Scassellati [2011].

### PROJECT C3. KINEMATIC SELF CALIBRATION

By starting from a known kinematic model, it is possible to compensate for errors by means of visuo-kinematic calibration.

### References

 * P. Rochat (1998). **Self-perception and action in infancy**. *Experimental Brain Research*. 1998
 * M. Hoffmann et al. (2010). **Body Schema in Robotics: A Review**. In: *IEEE Transactions on Autonomous Mental Development*. Vol. 2, No. 4, Dec 2010. [[PDF]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.357.6076&rep=rep1&type=pdf)
 * J. W. Hart and B. Scassellati (2011). **A Robotic Model of the Ecological Self**. In: *Proceedings of the 11th IEEE/RAS International Conference on Humanoid Robots (Humanoids 2011)*. Bled, Slovenia, October 2011. [[PDF]](http://scazlab.yale.edu/sites/default/files/files/hart-humanoids-11.pdf)
 * Tikhanoff et al (2013). **Exploring affordances and tool use on the iCub**. In *Proceedings of the 13th IEEE/RAS International Conference on Humanoid Robots (Humanoids 2013)*. [[PDF]](http://www.poeticon.eu/publications/1335_Tikhanoff_etal2013.pdf)

## Project D: Better control → _Reaching in clutter_

**Supervisor**: *Alessandro Roncone*
{% include video.html url="//www.youtube.com/embed/API96d56v3I" %}

### D1. PERCEPTION

   * Development of a perception algorithm (kinect-based) able to detect obstacles close to the robot's arms
     * Calibration of camera w.r.t. the robot
     * Detection of the robot arms inside the camera frame
     * Detection of robot - obstacle distances throughout the robot's body

### D2. CONTROL

   * Development of a suitable avoidance strategy for the robot 
     * Computation of avoidance vectors based on robot-obstacle distances (the one from [Flacco 2012] should suffice)
   * Deployment of the control algorithm on the Baxter/ROS platform

### Expected result

 * A publication
 * A cool demo

### References

 * A. De Luca and F. Flacco (2012). **Integrated control for pHRI: Collision avoidance, detection, reaction and collaboration**, in *Biomedical Robotics and Biomechatronics (BioRob), 2012 4th IEEE RAS EMBS International Conference on*. June 2012, pp. 288–295.
 * F. Flacco et al. (2012). **A depth space approach to human-robot collision avoidance**, in *Robotics and Automation (ICRA), 2012 IEEE International Conference on*. May 2012, pp.
338–345.
