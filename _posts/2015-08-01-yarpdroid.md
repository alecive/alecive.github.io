---
layout: post
title: Android integration onto the iCub platform
link: https://github.com/alecive/yarpdroid
link-alt: GitHub repository
modal-id: 3
img: yarpdroid2.png
alt: yarpdroid
date: 2015-08-01
category: research
description: 
article: yes
double: yes

---

Over the past month, I've been tinkering with Android Studio and tried to seamlessly integrate it with `yarp` in particular (and the `iCub` software architecture in general). I really believe that a robot can dramatically benefit from the number of sensors a smartphone is provided with. And this can be dual: better HRI, better feedback from the robot, and so on.

To this end, I worked (along with mainly Francesco Romano for some low-level Java support) on the cross-compilation of yarp on ARM-v7, and the implementation of a working JNI interface to switch back and forth from the Java layer and the C++ one. As a result, I developed an Android application (aptly named `yarpdroid`), which provides a template for some basic functionalities I worked on, as well as a couple of already available use-cases. The code is available at [https://github.com/alecive/yarpdroid](https://github.com/alecive/yarpdroid).

I'll update this post with more information

## Features

 * **Material Design** (because why not)
 * **Sending data** from the smartphone to the YARP network 
 * **Receiving data** from the smartphone to the YARP network 
 * **Sending images** from the smartphone to the YARP network 
 * **Receiving images** from the smartphone to the YARP network (**TODO**)
 * **Google Glass** interface for a couple of amazing things I will talk about later on

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

Videos are on their way!
