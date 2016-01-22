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


# Prerequisites

All of these prerequisites are not mandatory but helpful: they can be learned on the fly, but a prior familiarity with the topics will surely kick off the projects faster.

 * C++/Python development skills
 * Git/versioning systems (not mandatory, they can be learned on the go)
 * Basic knowledge of kinematics, computer vision, robotics, control, machine learning
 * Linux knowledge would be helpful (all the Baxter code runs on Ubuntu 14.04)
 * ROS

# Expected results

 1. Things you will learn (in random order):
   * ROS
   * robotics perception
   * robotics control
   * standard computer science skills 
   * machine learning (depending on project)
   * optimization techniques (depending on project)
 2. If all goes well, a publication for the senior projects is more than reasonable.
 3. A cool demo is always something to be proud of :)

# 6-month projects

## Project A: Improvements on the tictactoe demo

{% include image.html url="blog/baxter_tictactoe.jpg" width="width:90%;"  description="Baxter playing tictactoe." %}

**Robot**: *Baxter Research Robot* [[link]](http://www.rethinkrobotics.com/baxter-research-robot/)

**Supervisors**: *Alessandro Roncone, Olivier Mangin*

### Task A1. Perception

 * Code refactoring 
 * Automatic calibration of the board 
 * Automatic calibration of the HSV segmentation of the tiles

### Task A2. Action

 * Inverse Kinematics instead of recorded (predefined) actions (see [IKFast](https://goo.gl/MwyTXX) or [the SDK Wiki](http://sdk.rethinkrobotics.com/wiki/API_Reference#Inverse_Kinematics_Solver_Service))
 * Automatic calibration of the demo w.r.t. different table heights
 * Improvements on the vacuum gripper part
 * Better speech synthesizer 

## Project B: SnapCircuit Task

{% include image.html exturl="http://ecx.images-amazon.com/images/I/81sj9QjDChL._SL1500_.jpg" width="width:75%;"  description="SnapCircuit board with some parts." %}

**Robot**: *Baxter Research Robot* [[link]](http://www.rethinkrobotics.com/baxter-research-robot/)

**Supervisors**: *Alessandro Roncone, Olivier Mangin*

### Task B1. Perception

 * Automatic Board detection
 * Automatic segmentation of SnapCircuit Parts on the board
 * Automatic recognition of the topology of the board

### Task B2. Action

 * Inverse Kinematics for high level control of the end-effector (see [IKFast](https://goo.gl/MwyTXX) or [the SDK Wiki](http://sdk.rethinkrobotics.com/wiki/API_Reference#Inverse_Kinematics_Solver_Service))
 * Manipulation of the SnapCircuit Parts and their placement on the board

# Senior Projects

{% include video.html url="//www.youtube.com/embed/zegs0TSFF6A" description="State of the art in body representation and control"%}

> *To date, robot controllers largely concentrate on the end-point as the only part that enters in physical contact with the environment. The rest of the body is typically represented as a kinematic chain, the volume and surface of the body itself rarely taken into account. Sensing is dominated by “distal” sensors, like cameras, whereas the body surface is “numb”. As a consequence, reaching in cluttered, unstructured environments poses severe problems, as the robot is largely unaware of the full occupancy of its body, limiting the safety of the robot and the surrounding environment. **This is one of the bottlenecks that prevent robots from working alongside human partners.*** [Roncone et al. 2015]

## Project C: Better perception → _Self modeling_ 

**Robot**: *Baxter Research Robot* [[link]](http://www.rethinkrobotics.com/baxter-research-robot/)

**Supervisor**: *Alessandro Roncone*

> *...by 2-3 months, infants engage in exploration of their own body as it moves and acts in the environment. They babble and touch their own body, attracted and actively involved in investigating the rich intermodal redundancies, temporal contingencies, and spatial congruence of self-perception.* [Rochat, 1998]

### TASK C1. Learning the Kinematics

By starting with as little information as possible, it is possible to compute a reliable enough kinematic model from self-observation and exploration of the consequences of the robot's actions.

> *This process calibrates the robot's kinematic model to its vision model, producing a unified model that allows kinematic and visual information to be meaningfully combined. The presented model is demonstrated to predict end-effector position in the visual field. The robot further refines this combined kinematic-visual model by minimizing the distance between the predicted and observed positions of its end-effector in its visual field. The fact that the robot learns these properties based on first-hand observations of its body, through its sensors, allows the model to adapt to changes in the robot’s configuration on-line. This endows the robot with the ability to adapt its self-model for tool use.* [Hart and Scassellati, 2011]

### TASK C2. Exploring Tool Use and object affordances

I.e. if I am able to incorporate a new tool into my internal model, how can I exploit it in order to do new tasks?
In summary: what the robot is capable or not capable of doing after "training" with a tool, w.r.t. the previous experience.
See Hart and Scassellati [2011], Tikhanoff et al [2013].

### TASK C3. Kinematic self calibration

By starting from a known kinematic model, it is possible to compensate for systematic errors by means of visuo-kinematic calibration. It improves reaching and visual servoing - see Fanello et al. [2014].
Systematic errors include (i) mismatch between the robot model based on the mechanical design specifications (CAD model) and the actual physical robot; (ii) inaccuracies in joint sensor calibration and measurements; (iii) unobserved variables as for example backlash or mechanical elasticity; (iv) inaccuracies in taxel pose calibration; (v) errors in visual perception due to inaccurate camera calibration. The combination of these sources of error can amount to a total of several centimeters.

There is evidence that, in adult humans, sensory systems are not fixed structures with immutable functions. It is of course widely appreciated that sensory systems can be significantly modified by the input they receive during development. For example, to achieve optimal motor behavior for reaching and grasping, visual and somatic senses must be continually adjusted as different body parts grow at different pace. One might expect such adjustments to proceed very slowly and to be largely restricted to immature organisms, but there is evidence of strong sensory plasticity that can be evoked within minutes in adults. [Volcic et al. 2013]

### References

 * P. Rochat [1998]. **Self-perception and action in infancy**. *Experimental Brain Research*. 1998
 * M. Hoffmann et al. [2010]. **Body Schema in Robotics: A Review**. In: *IEEE Transactions on Autonomous Mental Development*. Vol. 2, No. 4, Dec 2010. [[PDF]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.357.6076&rep=rep1&type=pdf)
 * J. W. Hart and B. Scassellati [2011]. **A Robotic Model of the Ecological Self**. In: *Proceedings of the 11th IEEE/RAS International Conference on Humanoid Robots (Humanoids 2011)*. Bled, Slovenia, October 2011. [[PDF]](http://scazlab.yale.edu/sites/default/files/files/hart-humanoids-11.pdf)
 * M. Hersch et al [2008]. **Online Learning of the body schema**. In *International Journal of Humanoid Robotics*. Vol. 5, No. 2, 2008. [[PDF]](http://infoscience.epfl.ch/record/117918/files/IJHR_0502_P161.pdf)
 * Tikhanoff et al. [2013]. **Exploring affordances and tool use on the iCub**. In *Proceedings of the 13th IEEE/RAS International Conference on Humanoid Robots (Humanoids 2013)*. [[PDF]](http://www.poeticon.eu/publications/1335_Tikhanoff_etal2013.pdf)
 * S. R. Fanello et al. [2014]. **3D Stereo Estimation and Fully Automated Learning of Eye-Hand Coordination in Humanoid Robots**. In *Proceedings of the 14th IEEE/RAS International Conference on Humanoid Robots (Humanoids 2014)*. [[PDF]](http://alecive.github.io/papers/%5BFanello%20et%20al.%202014%5D%20-%203D%20estimation%20and%20fully%20automated%20learning%20of%20eye-hand%20coordination%20in%20humanoid%20robots.pdf)
 * R. Volcic et al. [2013]. **Visuomotor Adaptation Changes Stereoscopic Depth Perception and Tactile Discrimination**. In *The Journal of Neuroscience*, Oct 23, 2013.

## Project D: Better control → _Reaching in clutter_

**Robot**: *Baxter Research Robot* [[link]](http://www.rethinkrobotics.com/baxter-research-robot/)

**Supervisor**: *Alessandro Roncone*

{% include video.html url="//www.youtube.com/embed/API96d56v3I" description="From [Flacco et al. 2012]" %}

### D1. PERCEPTION

 * Development of a perception algorithm (kinect-based) able to detect obstacles close to the robot's arms
   * Calibration of camera w.r.t. the robot
   * Detection of the robot arms inside the camera frame
   * Detection of robot - obstacle distances throughout the robot's body

### D2. CONTROL

 * Development of a suitable avoidance strategy for the robot 
   * Computation of avoidance vectors based on robot-obstacle distances (the one from [Flacco 2012] should suffice)
 * Deployment of the control algorithm on the Baxter/ROS platform

### References

 * A. De Luca and F. Flacco [2012]. **Integrated control for pHRI: Collision avoidance, detection, reaction and collaboration**, in *Biomedical Robotics and Biomechatronics (BioRob), 2012 4th IEEE RAS EMBS International Conference on*. June 2012, pp. 288–295. [[PDF]](http://www.dis.uniroma1.it/~labrob/pub/papers/BioRob12.pdf)
 * F. Flacco et al. [2012]. **A depth space approach to human-robot collision avoidance**, in *Robotics and Automation (ICRA), 2012 IEEE International Conference on*. May 2012, pp.
338–345. [[PDF]](http://www-cs.stanford.edu/groups/manips/publications/pdfs/Flacco_2012_ICRA.pdf)

## Project E: Hands-free teleoperation

{% include video.html url="//www.youtube.com/embed/gtkrPhcYhyI" %}

**Robot(s)**: *Baxter research robot* [[link]](http://www.rethinkrobotics.com/baxter-research-robot/) and *KUKA youBot arm* [[link]](http://www.youbot-store.com/)

**Supervisor**: *Alessandro Roncone*

There are many previous works to take inspiration from (and many different techniques have been used). The basic principle is to be able to track the 6 degrees of freedom of the user's hand, and transfer them to the robot's end-effector (with a 6-DOF tracker the problem is fully determined).
The goal would be to develop a robot-agnostic platform (i.e. able to work on both the Baxter and the KUKA).

### Attack Plan

 1. Implement a ROS compatible, 6-DOF hand pose tracker.
 2. Implement (or use an existing) an Inverse Kinematic controller for both the robots.
 3. Interface the 6-DOF hand pose tracker with the IK controller.
 4. ...
 5. Profit!

*Disclaimer: if you didn't get the joke, it means you never saw [this video](https://www.youtube.com/watch?v=EmoCuA4-y9E)!*

### Stretch goals

 * Implement a face tracking system able to detect the user's face orientation (3DoF). It can be purely vision based (e.g. the [CLM tracker](https://github.com/TadasBaltrusaitis/CLM-framework)), or use some more complex systems (e.g. see this [Google Glass head teleoperation on the iCub robot](https://www.youtube.com/watch?v=Hw_Yw8LtZTE)).
 * Implement a head teleoperation system on the Baxter robot (2DoF, pan and tilt)
