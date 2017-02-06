---
layout: post
title: Kinematic Calibration
link:
link-alt:
date: 2016-04-30
category: blog
description: And its secrets
tags: [calibration,kinematics,how to,tutorial]
article: yes

---

# Contents
{:.no_toc}

* This line will be replaced by the ToC, excluding the "Contents" header
{:toc}

Practically all robots rely on models of their kinematics and dynamics. Their success is largely determined by the accuracy of such models. This is even more so if they operate with limited feedback, as it is often the case when we consider robots in real-time interaction with the environment. The models are typically based on mechanical design specifications (such as CAD drawings) of the robot. However, inaccuracies creep in in many ways as for example in the assembly process, in mechanical elasticity, or simply because of cheap design or components. Therefore, the actual model parameters of every robot exemplar have to be found by means of a calibration procedure.

In the following, I will be concerned with calibration of the standard *Denavit-Hartenberg* (DH) parameters that fully describe the robot's kinematics through a series of rotations and translations from the base of the robot up to the end-effector. I decided to write these things down for two reasons: i) there are no references that provide a full analysis of the problem in detail ii) it might be useful to others (including me if I am going to need it in the future).

# Disclaimer

Let me formulate some assumptions:

 * I will be focusing on the calibration of the **standard** DH parameters. For a good excerpt on the calibration of the modified DH parameters, please refer to the wonderful *Handbook of Robotics* [Siciliano and Khatib 2008].
 * I will not extensively describe the problem, but I will elaborate on what I found useful in the past from the consistent body of work that has been published on the topic.
 * Some of the paragraphs in this article are taken from my [2014 ICRA paper]({% post_url research/2014-06-08-doubleTouch %}), which you're kindly requested to cite if you find this page useful.

# Calibration Techniques

## 1.1 Circle Point Analysis (CPA)

Circular point analysis (CPA) is an early method used to perform kinematic calibration because of the straight forward nature of the calculation. CPA leverages the ability to control each given joint in a known sequence while holding all other joint angles or positions fixed and tracking at least one point distal to the joint being identified [7]. In terms of DH parameters, a revolute joint has a locus of points in a circle centered at the joint z-axis in a plane perpendicular to that
axis, while a translational joint has a locus of points that forms a line parallel to the z-axis In the case of the Powerball arm all joints are revolute. The accuracy of the CPA method for each joint is highly sensitive to the radial distance of the
track point from the joint axis. This is seen in equation 6.1 where as r goes to 0 equation 6.1 becomes degenerate as the points all overlap and fail to define a plane.

(x − x_0 ) 2 + (y − y_0 ) 2 + (z − z_0 ) 2 = r^2

One advantage of using the CPA method is that it only requires tracking discrete points and not the full pose of the end effector. This made the camera tracking process easier since tracking just the position of a body requires fewer track points than tracking the full pose of a rigid body [9]. In an attempt to extract some additional precision from the camera tracking system the orientation data was used to extrapolate the point location further from the joint axis. This showed large jumps in the position caused by orientation errors making this technique untenable for this analysis. There were two main sources of orientation error, one was the loss of track points during capture, the other was the configuration of track points was poor for orientation tracking because they formed a straight line making one axis of orientation near singular.

## 1.2 Gauss-Newton Method

## 1.3 Non-linear Optimization

The problem can be also defined in terms of a constrained optimization problem.

The software I usually choose is IPOPT, a public domain software package designed for large-scale nonlinear optimization problems. The reasons are multiple:

 * Simple and Flexible *C++ Interface*
 * *Open Source*, and freely available
 * *Quick Convergence*
 * *Scalability*
 * *Automatic Handling of singularities and parameters limits*
