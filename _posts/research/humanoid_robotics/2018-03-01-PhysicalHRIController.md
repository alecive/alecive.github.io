---
title: Real-time avoidance for Human-Robot Interaction
img: PhysicalHRIController.png
alt: Physical-HRI-Controller
description: Model set for Human-Robot collaborative tasks
tags: [research,robotics,baxter,hri,human robot interaction,collaborative manufacturing,human robot collaboration,advanced manufacturing,open source,github]
authors: Phuong D. H. Nguyen, Matej Hoffmann, Alessandro Roncone, Ugo Pattacini, and Giorgio Metta
submission: ACM/IEEE International Conference on Human-Robot Interaction (HRI2018), Chicago, IL, USA, March 5-8, 2018
paper_pdf: "2018_Nguyen_HRI_physical_hri_controller"
paper_title: "Compact real-time avoidance on a Humanoid Robot for Human-Robot Interaction"
---


{% include video.html url="//www.youtube.com/embed/A9Por3anPJ8" %}

We have developed a new framework for safe interaction of a robot with a human composed of the following main components (cf. Fig 1):

 1. a human 2D keypoints estimation pipeline employing a deep learning based algorithm, extended here into 3D using disparity;
 2. a distributed peripersonal space representation around the robot's body parts;
 3. a new reaching controller that incorporates all obstacles entering the robot's protective safety zone on the fly into the task.

{% include image.html url="portfolio/PhysicalHRIController_architecture.png" max-width="100%" description="<b><i>Figure 1</i></b>. Software architecture for physical human-robot interaction. In this work, we develop a framework composed of: i) a human pose estimation algorithm, ii) a 2D to 3D disparity mapping, iii) a peripersonal space collision predictor, iv) a pHRI robot controller for distributed collision avoidance." %}

Here's another video of the controller in action:

{% include video.html url="//www.youtube.com/embed/ArrwbhvKdew" description="Controller in action. The controller can seamlessly process both tactile (physical contact) and visual (prior-to-contact) information in order to avoid obstacles while still optimizing its trajectory to accomplish the primary reaching task." %}

The main novelty lies in the formation of the protective safety margin around the robot's body parts---in a distributed fashion and adhering closely to the robot structure---and its use in a reaching controller that dynamically incorporates threats in its peripersonal space into the task.
The framework is tested in real experiments that reveal the effectiveness of this approach in protecting both human and robot against collisions during the interaction.
Our solution is compact, self-contained (on-board stereo cameras in the robot's head being the only sensor), and flexible, as different modulations of the defensive peripersonal space are possible---here we demonstrate stronger avoidance of the human head compared to rest of the body.

