---
layout: post
title: A Cartesian 6-DoF Gaze Controller for Humanoid Robots
link: http://wiki.icub.org/iCub/main/dox/html/icub_gaze_interface.html
link-alt: Documentation and tutorials
img: gazeController.jpg
img-thumb: gazeController_thumb.jpg
alt: gaze-controller
date: 2016-07-07
category: research
description:
article: yes
tags: [research,robotics,icub,robot,humanoids,control,gaze stabilization,inertial sensor,imu,velocity control,whole body motion,walking,balancing,open source,github]
authors: Alessandro Roncone, Ugo Pattacini, Giorgio Metta, and Lorenzo Natale
submission: 2016 Robotics - Science and Systems, Ann Arbor, MI, U.S.A., June 18-22, 2016
paper_pdf: /papers/[Roncone et al. 2016] A Cartesian 6-DoF Gaze Controller for Humanoid Robots.pdf
paper_title: A Cartesian 6-DoF Gaze Controller for Humanoid Robots

---

## Description (excerpt from my RSS talk)

We have developed a 6 degrees of freedom (DoFs) gaze controller. Our goal is the control of the head of the iCub Humanoid robot, which is equipped with a three degrees of freedom neck and a three degrees of freedom binocular system capable of version and vergence behaviors. Potential applications range from the more standard tracking and attentive systems to image stabilization capabilities during whole body motions such as walking and balancing.

The current state of the art in gaze control is composed of systems characterized by exponential velocity profiles, with fast onset and slower decay toward the target. Our goal has been to improve these types of trajectories and implement smooth, minimum jerk, bell shaped velocity profiles that have been found to be typical of a human movement.

We defined the gaze problem as the task of controlling the head motors in order to move its fixation point toward a desired 3D position. As such, our task is inherently redundant, and for this reason, we have decided to implement a set of secondary behaviors to complement the main task, that is a vestibulo-ocular reflex, a gaze stabilization system, and saccadic behaviors.

{% include image.html url="portfolio/gazeController_architecture.svg" description="<b><i>Figure 1</i></b>. Block diagram of the presented framework." %}

The architecture we implemented is shown in Figure 1. The control task is decoupled into two independent subsystems, which account for the neck and the eyes respectively. For each of them, a two-stage design (consisting of an inverse kinematic solver and a velocity controller) computes the set of joint velocities needed for moving the fixation point from its current position to the desired target.
The additional behaviors listed above are added to the main goal if requested by the user.

Particular attention has been given to the design of the software interface that is exposed to the user, with flexibility in both the tuning of the internal parameters and the type of gaze target that can be asked for by the user. In conclusion, we have developed a comprehensive architecture for the explicit control of the fixation point of a generic binocular system. As a matter of fact, this software has been already ported to the Vizzy robot you can see in the picture. The software has been released with an open source license and it is freely available online.

## Video

{% include video.html url="//www.youtube.com/embed/I4ZKfAvs1y0" %}

## Slides

Here are the slides I used during the presentation at RSS2016:

{% include pdf.html url="portfolio/gazeController.pdf" description="Slides used at RSS2016" %}

