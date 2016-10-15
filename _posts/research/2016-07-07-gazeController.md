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

We have developed a 6 degrees of freedom (DoFs) gaze controller. Our goal is the control of the head of the iCub Humanoid robot, which is equipped with a 3-DoFs neck and a 3-DoFs binocular system capable of version and vergence behaviors. Potential applications range from the more standard tracking and attentive systems to image stabilization capabilities during whole body motions such as walking and balancing.

## Video

{% include video.html url="//www.youtube.com/embed/I4ZKfAvs1y0" %}

## Description (from my RSS talk)

The current state of the art in gaze control is composed of systems characterized by exponential velocity profiles, with fast onset and slower decay toward the target. Our goal has been to improve these types of trajectories and implement smooth, minimum jerk, bell shaped velocity profiles that have been found to be typical of a human movement.

We defined the gaze problem as the task of controlling the head motors in order to move its fixation point toward a desired 3D position. As such, our task is inherently redundant, and for this reason, we have decided to implement a set of secondary behaviors to complement the main task, that is a vestibulo-ocular reflex, a gaze stabilization system, and saccadic behaviors.

{% include image.html url="portfolio/gazeController_architecture.svg" description="<b><i>Figure 1</i></b>. Block diagram of the presented framework." %}

The architecture we implemented is shown in Figure 1. The control task is decoupled into two independent subsystems, which account for the neck and the eyes respectively. For each of them, a two-stage design (consisting of an inverse kinematic solver and a velocity controller) computes the set of joint velocities needed for moving the fixation point from its current position to the desired target.
The additional behaviors listed above are added to the main goal if requested by the user.

### Results

The control architecture depicted in Figure 1 has been implemented and released under the GPL open source license. As such, it is freely accessible on [GitHub](https://github.com/robotology/icub-main). It is developed for the iCub humanoid robot, and it is readily available for any iCub robot. Nonetheless, it is generically applicable to any humanoid head, and the code has been designed to be modular and easy to adapt to any other robotic platform (provided that a suitable kinematic representation is available). In this regard, a porting onto the 6-DoF head of the Vizzy robot [has been already carried out](http://mediawiki.isr.ist.utl.pt/wiki/Vizzy\_Cartesian\_Interface).

Particular attention has been given to the design of the software interface that is exposed to the user. For example, the desired target can be sent to the controller in different formats (e.g. either the 3D cartesian point to look at or a triangulation of the target coordinates in both the left and the right image frames). A configuration interface allows the user to tune the internal parameters of the Gaze Controller for a finer control of the software (e.g. enabling/disabling saccadic movements, triggering the neck stabilization on and off, tuning the execution time for the neck and eyes controllers, and so on).

Our experiments (see video above) demonstrate the capabilities of the system in handling different types of tasks. The Gaze Controller presented in this paper is able to successfully execute smooth pursuit behaviors and tracking of 3D points in space. Importantly, the additional capabilities added to the system proved to be advantageous under various circumstances. The saccadic behavior is able to quickly move the eyes toward the target when large gaze shifts are requested, whereas the vestibulo-ocular reflex uses the gyroscope readouts in order to compensate the neck movements, effectively maintaining the fixation point on target. Finally, the gaze stabilization system utilizes the feedback from the inertial measurement unit in order to reduce image blur both when the robot is subject to external disturbances, and during active gaze control.

## F.A.Q.

During the poster session subsequent to my RSS presentation, I got a number of questions that I thought would be worth adding to this page. They are listed below.

#### 1. If the control is decoupled, how do you choose if to move the neck or the eyes first?

In short, you don't: they both start at the same time (as humans do). The neck and the eyes are two completely independent subsystems that do not need to be synchronized or to communicate one another. As a matter of fact, this allows for gaze profiles similar to humans. The faster dynamics of the eyes let the subject rapidly catch the target; after a while, the neck starts moving toward the fixation target, while the VOR reflex occurring at the eyes maintain the fixation point on the target by compensating the neck movements (cf. Figure 2).

{% include image.html url="portfolio/gazeController_gazeshifts.svg" description="<b><i>Figure 2</i></b>. Qualitative comparison between a gaze shift performed by the Gaze Controller on the iCub (left), and a typical gaze shift in healthy human subjects (right). In both graphs, angular displacements of neck, eyes, and gaze are shown with respect to time." %}

This effectively helps in the context of human-robot interaction. The head and eye movements are a highly communicative part of the human body, and endowing a robotic system with similar behaviors equips the robot with higher predictability and better integration with the human partner. The effectiveness of the proposed control framework in signaling non-verbal cues during human-robot interaction has been analyzed in related work [[Boucher 2012]](https://www.ncbi.nlm.nih.gov/pubmed/22563315). They demonstrated how naive human subjects are sensitive to gaze in the context of cooperative tasks, effectively improving their performance if a meaningful gazing information from the robot is provided.

#### 2. How do you control the robot without planning?

#### 3. Why do you need such a complex machinery when you can use a much simpler hardware?



## Slides

Here are the slides I used during the presentation at RSS2016:

{% include pdf.html url="portfolio/gazeController.pdf" description="Slides used at RSS2016" %}

