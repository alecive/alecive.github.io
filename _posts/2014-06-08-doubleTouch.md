---
layout: post
title: Automatic kinematic calibration using artificial skin via double Touch
link: https://github.com/alecive/periPersonalSpace
link-alt: GitHub repository
img: doubleTouch.png
alt: double-touch
date: 2014-06-08
category: research
description: 
tags: [research,robotics,icub,robot,humanoids,double touch,self touch,inverse kinematics,denavit-hartenberg,dh parameters,ipopt,optimization,cognitive robotics,body representations,icra,icra 2014,body schema,open source,github]
article: yes

---

### Reference paper: _Automatic kinematic chain calibration using artificial skin: self-touch in the iCub humanoid robot_ <a class="no-print" href="/papers/[Roncone et al. 2014] - Automatic Kinematic Chain Calibration using artificial skin: self-touch in the iCub humanoid robot.pdf" target="_blank"> [PDF]</a>

**Authors:** _Alessandro Roncone, Matej Hoffmann, Ugo Pattacini, and Giorgio Metta_

**Submission:** _IEEE International Conference on Robotics and Automation (ICRA2014), Hong Kong, China, May 31-June 7, 2014_

## Video

Here is a video that summarizes the behavior:

{% include video.html url="//www.youtube.com/embed/pfse424t5mQ"%}

## Description

This project deals with the task of solving the problem of _self-(or double-)touch_. It is defined as the robot being able to touch itself on a specific region of the skin, and it represents an unprecedented opportunity for a humanoid robot to achieve the simultaneous activation of multiple skin parts (in the video above, patches belonging to the right hand and the left forearm). This high amount of information was then used later on for exploiting a completely autonomous calibration of the body model (i.e. kinematic calibration or tactile calibration). In the reference paper cited above, this competence has been used to perform a kinematic calibration of both the right and the left arms.

The _self-touch_ or _double-touch_ scenario has been further developed and used for collecting tactile and proprioceptive data that serve kinematic calibration. In robotics, this constitutes a novel solution to the self-calibration problem, in which no external metrology (like cameras or other tracking apparatus) is necessary. The kinematic chain is closed through touching its own body: the correspondence between the predicted contact point from existing forward kinematics and the actual position on the robot's "skin" provides sample data that allows simultaneous learning of the kinematic representation as well as the position of individual tactile sensors (taxels). The existing iCub kinematic model (DH parameters) and initial calibration of the tactile array served as a starting point and we have successfully improved on these. The data collection procedure is automated - self-touch is autonomously executed by the robot - and can be repeated at any time, providing a compact self-calibration system. 

At present, the visual modality is being added, employing modules that already exist for the iCub (object tracking, gaze controller, stereo vision). This will allow for automatic calibration of additional components of the system: head and eye kinematics, the stereo pair, and camera projective maps. Furthermore, in collaboration with Bielefeld University, we are improving the autonomy and robustness of the double-touch behavior by using visual and tactile servoing.

## Slides

Here are the slides I used during the presentation at ICRA2014:

{% include pdf.html url="portfolio/doubleTouch.pdf" description="Slides used at ICRA2014" %}

## Paper Abstract

Calibration continues to receive significant attention in robotics because of its key impact on performance and cost associated with the operation of complex robots. Calibration of kinematic parameters is typically the first mandatory step. To this end, a variety of metrology systems and corresponding algorithms have been described in the literature relying on measurements of the pose of the end-effector using a camera or laser tracking system, or, exploiting constraints arising from contacts of the end-effector with the environment.
In this work, we take inspiration from the behavior of infants and certain animals, who are believed to use self-stimulation or self-touch to “calibrate” their body representations, and present a new solution to this problem by letting the robot close the kinematic chain by touching its own body. The robot considered in this paper is sensorized with tactile arrays for a total of about 4200 sensing points. The correspondence between the predicted contact point from existing forward kinematics and the actual position on the robot’s ‘skin’ provides sample data that allows refining the kinematic representation (DH parameters). The data collection procedure is automated — self-touch is autonomously executed by the robot — and can be repeated at any time, providing a compact self-calibration system that does not require an external measurement apparatus.
