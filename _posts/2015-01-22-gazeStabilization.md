---
layout: post
title: gaze Stabilization for humanoid robots
link: https://github.com/alecive/gaze-stabilization
link-alt: GitHub repository
img: gazeStabilization.png
alt: gaze-stabilization
date: 2015-01-22
category: research
description: 
article: yes

---

#### Reference paper: _Gaze Stabilization for Humanoid Robots: a Comprehensive Framework_ <a class="no-print" href="/papers/[Roncone et al. 2014] - Gaze stabilization for humanoid robots: a Comprehensive Framework.pdf" target="_blank"> [PDF]</a>

**Authors:** _Alessandro Roncone, Ugo Pattacini, Giorgio Metta, and Lorenzo Natale_

**Submission:** _2014 IEEE-RAS International Conference on Humanoid Robots, Madrid, Spain, November 18-20, 2014_

## Video

Here is a video that summarizes the behavior:

{% include video.html url="//www.youtube.com/embed/NSGea-tCLZM" %}

## Description

We have developed a framework for gaze stabilization on the iCub robot. The system uses all 6 degrees of freedom (DoF) of the head and it relies on two sources of information: (1) the inertial information read from the gyroscope mounted in the robot’s head (feedback) and (2) an equivalent signal computed from the commands issued to the motors of the torso (feedforward). For both cues we compute the resulting perturbation of the fixation point and use the Jacobian of the iCub stereo system to compute the motor command that compensates the perturbation (see <b><i>Figure 1</i></b>). Retinal slip (i.e. optical flow) is used to measure the performance of the system.

{% include image.html url="portfolio/gazeStabilization-blockDiagram.svg" description="<b><i>Figure 1</i></b>. Block diagram of the framework proposed for the gaze stabilization. The Gaze Stabilizer module (in green) is designed to operate both in presence of a kinematic feedforward (kFF) and an inertial feedback (iFB). In both cases, it estimates the motion of the fixation point and controls the head joints in order to compensate for that motion." %}

We define the stabilization problem as the stabilization of the 3D position of the fixation point  of the robot. It is achieved by controlling the cameras to keep the velocity equal to zero. The velocity of the fixation point is 6-dimensional, and, for this reason, a proper gaze stabilization can take place only if all the 6 DoFs of the neck+eye system are used (cf. <b><i>Figure 2</i></b>). A diagram of the proposed framework is presented in <b><i>Figure 1</i></b>. The gaze stabilization module has been designed to operate in two (so far mutually exclusive) scenarios:

 * A <i>kinematic feed-forward (kFF)</i> scenario, in which the robot produces self-generated disturbances due to its own motion; in this case motor commands predict the perturbation of the fixation point and can be used to stabilize the gaze.
 * An <i>inertial feed-back (iFB)</i> scenario, in which perturbations are (partially) estimated by an Inertial Measurement Unit (IMU). 

As result, the Gaze Stabilizer is realized by the cascade of two main blocks: the first block is used for estimating the 6D motion of the fixation point by means of the forward kinematics, while the latter exploits the inverse kinematics of the neck-eye plant in order to compute a suitable set of desired joint velocities able to compensate for that motion. The forward kinematics block represents a scenario-dependent component, meaning that its implementation varies according to the type of input signal (i.e. feedforward or feedback). Conversely, the inverse kinematics module has a unique realization.

{% include image.html url="portfolio/gazeStabilization-icubHeadKin.svg" width="width:75%;" description="<b><i>Figure 2</i></b>. Kinematics of the iCub’s torso and head. The upper body of the iCub is composed of a 3 DoF torso, a 3 DoF neck and a 3 DoF binocular system, for a total of 9 DoF. Each of these joints, depicted in red, are responsible for the motion of the fixation point. The Inertial Measurement Unit (IMU) is the green rectangle placed in the head; its motion is not affected by the eyes." %}

To fulfill our requirements, we provide a mathematical formulation for the forward and differential kinematics of the fixation point of a generic stereo system, in order to compute the position of the fixation point and its Jacobian matrix.

## Experiments

To validate our work we set up two experiments:

 * <i>Exp. A:</i> compensation of self-generated motion: we issue a predefined sequence at the yaw, pitch, and roll of the torso and test both the kFF and the iFB conditions carrying out a repeatable comparison between the two.
 * <i>Exp. B:</i> compensation in presence of an external perturbation: the motion of the fixation point is caused by the experimenter who physically moves the torso of the robot. In this case there is no feedforward signal available, and the robot uses only the iFB signal.

For each experiment, two different sessions have been conducted: in the first session the robot stabilizes the gaze only with the eyes, while in the second session it uses both the neck and the eyes. In both the scenarios, a session without compensation has been performed and used as a baseline for comparison. It is worth noticing that Experiment A is obviously a more controlled scenario, and for this reason we have used it to obtain a quantitative analysis. In Experiment B instead the disturbances are generated manually, and, as such, it is provided only a qualitative assessment of the performance of the iFB modality. For validation we use the dense optical flow measured from the cameras (cf. <b><i>Figure 3</i></b>). This can be used as an external, unbiased measure because it is not used in the stabilization loop.

## Results

{% include image.html url="portfolio/gazeStabilization-baselineVSinertial.jpg" description="<b><i>Figure 3</i></b>. Optical flow during an experimental session. <i>(left)</i> baseline experiment (no stabilization) <i>(right)</i> experiment with the feedback measurement coming from the inertial measurement unit (IMU)." %}

We demonstrate a significant improvement of the stabilization with respect to the baseline (68.1% on average). As expected, the system performs better in the kFF condition than in the the iFB case (23.1% on average): this is because in the former case the system uses a feedforward command that anticipates and better compensates for the disturbances at the fixation point. Furthermore, by exploiting all 6 DoFs in the head, the performance of the system improves by 24.4% on average. 
We show that the feedforward component allows for better compensation of the robot’s own movements and, if properly integrated with inertial cues, may contribute to improve performance in presence of external perturbations. We also show that the DoF of the neck must be integrated in the control loop to achieve good stabilization performance.
