---
layout: post
title: Android integration onto the iCub platform
link: https://github.com/alecive/yarpdroid
link-alt: GitHub repository
modal-id: 3
img: yarpdroid.png
alt: yarpdroid.png
date: 2015-08-01
category: research
description: 
article: yes
double: yes

---

Over the past month, I've been tinkering with Android Studio and tried to seamlessly integrate it with `yarp` in particular (and the `iCub` software architecture in general). I really believe that a robot can dramatically benefit from the number of sensors a smartphone is provided with. And this can be dual: better HRI, better feedback from the robot, and so on.

To this end, I worked (along with mainly Francesco Romano for some low-level Java support) on the cross-compilation of yarp on ARM-v7, and the implementation of a working JNI interface to switch back and forth from the Java layer and the C++ one. As a result, I developed an Android application (aptly named `yarpdroid`), which provides a template for some basic functionalities I worked on, as well as a couple of already available use-cases. The code is available at [https://github.com/alecive/yarpdroid](https://github.com/alecive/yarpdroid).

A quick tutorial on how to cross-compile YARP is provided here: (http://alecive.github.io/blog/2015/08/31/YARP-Cross-Compilation/)

## Features

### YARPdroid application

 * Nice **Material Design** interface (because why not)
 * **Google Glass** interface for a couple of amazing things I will talk about later on

### JNI Interface

The JNI interface has been a real mess. It required the cross-compilation of the YARP core libraries (for now, `YARP_OS`, `YARP_init`, and `YARP_sig`), which was no small feat. I'll upload any of the steps required to do this from scratch, but right now there are pre-compiled libraries in the GitHub repository in order to ease the process. What I managed to do was:

 * **Sending data** (of any kind) from the smartphone to the YARP network 
 * **Receiving data** (of any kind) from the smartphone to the YARP network 
 * **Sending images** from the YARP network to the smartphone (e.g. iCub's cameras)

The only thing that is missing in order to provide a complete template application is sending images from the smartphone to the YARP network. It is a not easy task, but we're working on it :

## Screenshots

<div class="row">
  <div class="col-sm-6">
    {% include image.html url="portfolio/yarpdroid_speechtotext.png" description="<b><i>Speech-to-text</i></b> interaction running on the application. This can be sent onto the YARP network to perform a variety of tasks (e.g. verbal interaction with the robot)." %}
  </div>
  <div class="col-sm-6">
    {% include image.html url="portfolio/yarpdroid_view.png" description="<b><i>Camera Viewers</i></b> from the robot: it is possible to send image data from the YARP network onto the smartphone in order to <i>'see with iCub's eyes'</i>" %}
  </div>
</div>


## Videos

Videos are on their way! I'll update this section from time to time.

#### Video #1

In this video, I show what happens if you empower users with a natural human-robot interface. The user can see what the robot sees, and it can direct its gazing by simply clicking on points into the image. Pretty neat!

{% include video.html url="//www.youtube.com/embed/1N0xf2_C6I0" %}

#### Video #2

In this super-lowres video, android speech recognition is integrated onto the iCub platform in order to provide a natural interface with the human user. Sorry for the quality!

{% include video.html url="//www.youtube.com/embed/s_qNTg448HA" %}
