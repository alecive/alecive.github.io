---
layout: post
title: double Touch
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

#### Submission: _ICRA 2014 Conference_

## Abstract

Calibration continues to receive significant attention in robotics because of its key impact on performance and cost associated with the operation of complex robots. Calibration of kinematic parameters is typically the first mandatory step. To this end, a variety of metrology systems and corresponding algorithms have been described in the literature relying on measurements of the pose of the end-effector using a camera or laser tracking system, or, exploiting constraints arising from contacts of the end-effector with the environment.
In this work, we take inspiration from the behavior of infants and certain animals, who are believed to use self-stimulation or self-touch to “calibrate” their body representations, and present a new solution to this problem by letting the robot close the kinematic chain by touching its own body. The robot considered in this paper is sensorized with tactile arrays for a total of about 4200 sensing points. The correspondence between the predicted contact point from existing forward kinematics and the actual position on the robot’s ‘skin’ provides sample data that allows refining the kinematic representation (DH parameters). The data collection procedure is automated — self-touch is autonomously executed by the robot — and can be repeated at any time, providing a compact self-calibration system that does not require an external measurement apparatus.

<!-- {% include video.html url="//www.youtube.com/embed/hoA9Dc7YEg4" description="doubleTouch on the iCub" %} -->

## Slides

Here are the slides I used during the presentation at ICRA2014:

{% include pdf.html url="portfolio/doubleTouch.pdf" description="Slides used at ICRA2014" %}