---
title: Transparency and Coordination in Human-Robot Collaboration
link: https://github.com/scazlab/baxter_collaboration
link-alt: GitHub repository
img: BaxterRoleAssignment.jpg
img-thumb: BaxterRoleAssignment_thumb.jpg
alt: baxter-role-assignment
category: research
description:
tags: [research,robotics,baxter,hri,human robot interaction,collaborative manufacturing,human robot collaboration,advanced manufacturing,open source,github]
type: article
authors: Alessandro Roncone, Olivier Mangin, and Brian Scassellati
submission: IEEE International Conference on Robotics and Automation (ICRA2014), Singapore, May 29-June 3, 2017
paper_pdf: "[Roncone et al. 2017] Transparent Role Assignment and Task Allocation in Human Robot Collaboration"
paper_title: "Transparent Role Assignment and Task Allocation in Human Robot Collaboration"

---

## Video
{: class="no-print"}

{% include video.html url="//www.youtube.com/embed/l6alHuMqx6Y" %}

## Description

Collaborative robots promise to increase productivity and improve working conditions.
Although modern robotic systems have become safe and reliable enough to operate close to human workers on a day-to-day basis, the workload is still skewed in favor of a limited contribution from the robot's side, and a significant cognitive load is allotted to the human.
We believe the transition from robots as recipients of human instruction to robots as capable collaborators hinges around the implementation of **transparent systems**, where mental models about the task are shared between peers, and the human partner is freed from the responsibility of taking care of both actors.
In this work, we implement a transparent task planner able to be deployed in realistic, near-future applications. The proposed framework is capable of basic reasoning capabilities for what concerns role assignment and task allocation, and it interfaces with the human partner at the level of abstraction he is most comfortable with. The system is readily available to non-expert users, and programmable with high-level commands in an intuitive interface. Our results demonstrate an overall improvement in terms of completion time, as well as a reduced cognitive load for the human partner.

## Method

We target robotic systems that are readily available to non-expert users. In this respect, a **hierarchical task model (HTM)** serves as the entry point for such users: it models the task with the same level of abstraction that one would use to describe the task to another person, while hiding the details of the implementation (cf. Fig. 1).

{% include image.html url="portfolio/BaxterRoleAssignment_htn.png" max-width="100%" description="<b><i>Figure 1</i></b>. HTM for high-level task representation. The user can inspect the task at various levels of granularity, and get feedback from the robot about its estimate of the current subtask (cyan block in picture)." %}

The first contribution of this work is a system able to convert high-level hierarchical models into low-level task planners capable of being executed by the robot. We propose to transform high-level HTMs into low-level, on-line planners by using **POMDPs**.
We consider here the extreme situation of a *blind robot* that is not capable of observing the actions of the human. This forces us to investigate mechanisms of coordination  though communication only.

We propose an automated technique able to transform task-level HTMs into low-level POMDPs. We focus on the optimal exploitation of communication as a (costly) way to reduce uncertainty on the system without affecting its state.
To fulfill this goal, we convert each primitive subtask (that is, each leaf composing the HTM in Fig. 1) into a small, modular POMDP, which we call a **restricted model** (RM [[Shani2014](http://ieeexplore.ieee.org/document/6494590/)]). Hence, the RMs are mostly independent from the rest of the problem and can be studied in isolation. Differently from [Shani2014](http://ieeexplore.ieee.org/document/6494590/), each RM is then composed at a later stage and the problem is solved in its entirety. This approach benefits from the modularity of the HTM representation, without the typical sub-optimality of policies that do not consider the full problem.

## Experimental Setup

We implemented our system on a Baxter Research Robot (cf. Fig. 2), using the Robot Operating System ([ROS](http://www.ros.org)). We devised a set of basic capabilities in order for the robot to be an effective partner. To this end, we implemented two low-level, state-less controllers (one for each of the robot's arms) able to operate in parallel and to communicate one another if needed.
A library of high-level predefined actions (in the form of ROS services) is available for the POMDP planner to choose from. Inverse kinematics is provided by _TRAC IK_ [[Beeson2015](http://ieeexplore.ieee.org/document/7363472/)], an efficient, general-purpose library that has been adapted to the Baxter robot and guarantees a control rate of `100Hz`.
For both controllers, the perception system is based on _ARuco_ [[Garrido-Jurado2014](http://www.sciencedirect.com/science/article/pii/S0031320314000235)], an OpenCV-based library able to generate and detect fiducial markers.

The system allows for context-based, multi-modal interactions with the user. Multiple, redundant communication channels are exposed by the framework, with the goal of interacting with the user on _human terms_ [[Breazeal2002](http://dlia.ir/Scientific/e_book/Technology/Engineering_Civil_Engineering_(General)/TA_166_167_Human_Engineering_/020286.pdf)]. This redundancy aims at allowing the human partner to choose the interface that suits him the most; importantly, it also has the advantage of making the interaction itself more robust.

## Experiment Design

In our experiment, the human and the robot are engaged in the joint construction of flat-pack furniture---specifically a stool (cf. Fig. 2).
It is worth noting how, although simple, this experiment represents an ideal scenario to evaluate the proposed approach: we purposely chose a task that does not require any particular skill from the human partner, but where the roles of both the human and the robot are decidedly clear.

The metric used to assess the effectiveness of our approach is the _completion time_ that the overall human-robot collaborative system takes to complete the task. We compare our proposed system (**Exp B**) against a control condition (**Exp A**), where the human operator actively asks for specific actions to be performed by the robot through a web interface.
A series of snapshots illustrating the task is shown in Fig. 2.

{% include image.html url="portfolio/BaxterRoleAssignment_snippets.png" max-width="100%" description="<b><i>Figure 2</i></b>. Snapshots acquired during the collaborative assembly of the stool in the control condition (top) and the interactive condition (bottom)." %}

## Results

The framework has been released under the `LGPLv2.1` open-source license, and it is freely accessible on [https://github.com/scazlab/baxter_collaboration](github.com/scazlab/baxter\_collaboration) for the Baxter's controllers, and [https://github.com/scazlab/task-models](github.com/scazlab/task-models) for the HTM to POMDP planner.
Although the majority of the codebase is robot-independent, the control architecture is readily available for any Baxter robot.

We test the proposed system in a proof-of-concept scenario in which the human and the robot are engaged in the joint construction of a stool. The system has been evaluated with 8 participants, in a within-subjects design.
Overall, the results suggest evidence of an improvement in terms of task efficiency: two-samples t-test between conditions A and B shows statistically significant difference, with a p-value of `0.016`.

Finally, we have registered a general user preference toward the proposed system. Multiple reasons were given that support the idea that a more transparent interaction favors the collaboration between peers. Most of the comments suggested a reduced cognitive load as the reason for such preference. Please refer to the paper for further information.

## Discussion

In this work, we demonstrate how high level task models can be combined with adaptive planning under uncertainty, as modeled by POMDPs. We propose a framework in which the robot autonomously intercedes for the human during the decision making step. Importantly, the system is completely transparent to the user, who is in full control of both the decisions made by the robot, and its operations during execution.

It is worth noting that in all the conditions the user was provided with minimal information regarding the capabilities of the framework. Indeed, the ability of the proposed system to intuitively interact with the human partner is considered an important asset of the proposed approach.
