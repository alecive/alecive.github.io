---
layout: post
title: Automatic kinematic calibration using artificial skin via double Touch
link: https://github.com/alecive/periPersonalSpace
link-alt: GitHub repository
modal-id: 3
img: doubleTouch.png
alt: double-touch
date: 2014-06-08
category: research
description: 
article: yes

---

#### Reference paper: _Automatic kinematic chain calibration using artificial skin: self-touch in the iCub humanoid robot_

#### Authors: _Alessandro Roncone, Matej Hoffmann, Ugo Pattacini, and Giorgio Metta_

#### Submission: _IEEE International Conference on Robotics and Automation (ICRA2014), Hong Kong, China, May 31-June 7, 2014_

## Video

Here is a video that summarizes the behavior:

{% include video.html url="//www.youtube.com/embed/pfse424t5mQ" description="This video deals with the task of solving the problem of self-(or double-)touch. This behaviour is defined as the robot being able to touch itself on a specific region of the skin, and it represents an unprecedented opportunity for a humanoid robot to achieve the simultaneous activation of multiple skin parts (in this video, patches belonging to the right hand and the left forearm). This high amount of information can be then used later on for exploiting a completely autonomous calibration of the body model (i.e. kinematic calibration or tactile calibration). In the reference paper cited above, this competence has been used to perform a kinematic calibration of both the right and the left arms." %}

## Slides

Here are the slides I used during the presentation at ICRA2014:

{% include pdf.html url="portfolio/doubleTouch.pdf" description="Slides used at ICRA2014" %}

## Abstract

Calibration continues to receive significant attention in robotics because of its key impact on performance and cost associated with the operation of complex robots. Calibration of kinematic parameters is typically the first mandatory step. To this end, a variety of metrology systems and corresponding algorithms have been described in the literature relying on measurements of the pose of the end-effector using a camera or laser tracking system, or, exploiting constraints arising from contacts of the end-effector with the environment.
In this work, we take inspiration from the behavior of infants and certain animals, who are believed to use self-stimulation or self-touch to “calibrate” their body representations, and present a new solution to this problem by letting the robot close the kinematic chain by touching its own body. The robot considered in this paper is sensorized with tactile arrays for a total of about 4200 sensing points. The correspondence between the predicted contact point from existing forward kinematics and the actual position on the robot’s ‘skin’ provides sample data that allows refining the kinematic representation (DH parameters). The data collection procedure is automated — self-touch is autonomously executed by the robot — and can be repeated at any time, providing a compact self-calibration system that does not require an external measurement apparatus.
