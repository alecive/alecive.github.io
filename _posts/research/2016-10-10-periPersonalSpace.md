---
layout: post
title: Visuo-tactile integration and margin of safety around the body
link: https://github.com/alecive/periPersonalSpace
link-alt: GitHub repository
img: periPersonalSpace.jpg
img-thumb: periPersonalSpace_thumb.jpg
alt: peripersonal-space
date: 2016-10-10
category: research
description:
tags: [research,robotics,icub,robot,humanoids,artificial skin,peripersonal space,visuo-tactile,multisensory integration,sensor fusion,parzen windows,cognitive robotics,body representations,iros,iros 2015,open source,github]
article: yes
authors: Alessandro Roncone, Matej Hoffmann, Ugo Pattacini, Luciano Fadiga, and Giorgio Metta
submission: 2016 PLOS ONE
paper_pdf: "[Roncone et al. 2016] Peripersonal Space and Margin of Safety around the Body: Learning Visuo-tactile Associations in a Humanoid Robot with Artificial Skin"
paper_title: "Peripersonal Space and Margin of Safety around the Body: Learning Visuo-tactile Associations in a Humanoid Robot with Artificial Skin"

---

### Conference paper: _Learning peripersonal space representation through artificial skin for avoidance and reaching with whole body surface_ <a class="no-print" href="{{ site.url }}/papers/[Roncone et al. 2015] - Learning peripersonal space representation through artificial skin for avoidance and reaching with whole body surface.pdf" target="_blank"> [PDF]<a class="no-print" href="{{ site.url }}/papers/[Roncone et al. 2015] - Learning peripersonal space representation through artificial skin for avoidance and reaching with whole body surface.bib" target="_blank"> [BIB]</a>

**Authors:** _Alessandro Roncone, Matej Hoffmann, Ugo Pattacini, and Giorgio Metta_

**Submission:** _2015 IEEE/RSJ International Conference on Intelligent Robots and Systems, Hamburg, Germany, September 28-October 2, 2015_

## Video
{: class="no-print"}

{% include video.html url="//www.youtube.com/embed/scaFDZZnIZs" %}

## Description

The **peripersonal space** (PPS) is a model of the nearby space that is of special relevance for the life of any complex animal. It is defined as the space surrounding our bodies, and is best described as a multisensory and sensorimotor interface with a fundamental role in the sensory guidance of actions. Owing to it is the ability to perform timely and appropriate actions toward objects located in the nearby space, which is critical for the survival of every animal. Depending on context, these actions may constitute an approaching or an avoidance behavior. In the case of defensive behavior, this creates a _margin of safety_ around the body, such as the flight zone of grazing animals or the multimodal attentional space that surrounds the skin in humans [[Graziano2006](https://www.princeton.edu/~graziano/Neuropsychologia_2006.pdf)].
Peripersonal space thus deserves special attention and probably justifies the specific neural circuitry devoted to its representation. The brain has to dynamically integrate information coming from several modalities being these motoric, visual, auditory or somatosensory [[Graziano2006](https://www.princeton.edu/~graziano/Neuropsychologia_2006.pdf),[Holmes2004](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1350799/)].
In animals and humans, PPS representations are gradually formed through physical interaction with the environment and in a complex interplay of body growth and neural maturation processes. _Self-touch_ (also called double-touch) is presumably one of the behaviors that impact the formation of multimodal body representations [[Rochat1998](http://www.psychology.emory.edu/cognition/rochat/lab/self-perception%20and%20action%20in%20infancy.pdf)]. They occur across different motor and sensory modalities, with the motor/proprioceptive and tactile starting already in prenatal stage. Vision is presumably incorporated later, during the first months after birth hand in hand with the maturation of the visual system. Perhaps even later, contingencies will encompass external objects.

{% include image.html url="portfolio/periPersonalSpace-iCub.svg" description="<b><i>Figure 1</i></b>. <b>(left)</b> double-touch behavior with a schematic of the kinematics and joint angles. <b>(right)</b> An object approaching the left forearm. Tracking of the object employs an optical flow tracker." %}

This simplified developmental timeline constitutes the skeleton of our work in the iCub humanoid, a robot with human-like morphology and a subset of the sensory capacities of the human body [[Metta2010](http://www.sciencedirect.com/science/article/pii/S0893608010001619)]. Lately, it has been equipped with a set of tactile sensors, which provide information about local pressure upon contact.
We model peripersonal space on the iCub by focusing on the integration of visual and tactile inputs. Our work shows how this representation can be learned following a developmental progression, starting with the robot exploring its own body by self-touch [[Roncone2014]({% post_url research/2014-06-08-doubleTouch %})] and registering correlations in motor and tactile spaces. Subsequently, visual information – derived from self-observation – kicks in and makes provision for learning multimodal responses. Then, learning is extended to other objects nearing and contacting the robot's body (Fig. 1).
Our model keeps in register each "spatial" visual receptive field (RF) to a taxel (tactile element) of the robot's skin. RFs are proxies for the neural responses, each of them represented by a probability density function. Probabilities are updated incrementally and carry information about the likelihood of a particular stimulus (e.g. an object approaching the body) eventually contacting the specific taxel at hand. We use the distance to the taxel `D` and its time to contact `TTC` to compactly identify the stimulus in a bi-dimensional parameter space.

This representation naturally serves the purpose of predicting contacts with any part of the body of the robot, which is of clear behavioral relevance. Furthermore, we implemented an avoidance controller whose activation is triggered by this representation, thus endowing the iCub with a _margin of safety_. Finally, minor modifications to the controller result in a reaching behavior that can use any body part as the end effector.

## Results

A volume was chosen to demarcate a theoretical visual _"receptive field"_ around every taxel (Figure 1). Learning then proceeded in a distributed, event-driven manner—every taxel stored and continuously updated a record of the count of positive (resulting in contact) and negative examples it has encountered for every combination of distance (`D`) and time to contact (`TTC`).

Selected results - for one taxel of left forearm - are shown in Figure 2. They show the representation after learning and smoothing using adapted Parzen Window method with color coding the third dimension (the estimated **probability of contact**). A clear "ridge" can be seen in the plot which corresponds to the trajectories of objects as they approach the taxel and both D and TTC are decreasing. The contact with the taxel occurs at both D and TTC approximatively equal to 0.

{% include image.html url="portfolio/periPersonalSpace-OpticalFlow_FAL_int2.png" max-width="50%" description="<b><i>Figure 2</i></b>. Spatial representation learned from oncoming objects - inner part of left forearm." %}

## Conclusions

This work is promising for future applications: with robots leaving the factory and entering less controlled domains, possibly sharing the space with humans, safety is paramount and multimodal awareness of the body surface and the space surrounding it is fundamental.
The proposed method can be employed for **life-long incremental learning** in the robot, automatically incorporating robot's new experiences or changes to its body or sensory apparatus. The robot can profit from this representation in that it provides a prediction of contacts with the skin prior to the actual contact.
An important feature is that learning is fast, proceeds in parallel for the whole body, and is incremental. That is, minutes of experience with objects moving toward a body part produce a reasonable representation in the corresponding taxels that is manifested in prior to contact activations.

The robotics implementation departs in many respects from the mechanisms that presumably operate in the primate brain. The correspondence between biology and robotics is established at a behavioral level rather than in the details of the implementation. In particular, for mostly practical reasons, we assume that the robot's kinematics and mapping of tactile information into reference frames is given from hand-coded models. The implementation of the double-touch behavior itself is taken as a primitive [[Roncone2014]({% post_url research/2014-06-08-doubleTouch %})]. Conversely, learning / calibration of the spatial receptive fields around individual taxels is primarily addressed here and relates to biology.
