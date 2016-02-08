---
layout: post
title: How to install ROS indigo
link: 
link-alt: 
date: 2015-11-12
category: blog
description: From a completely naive user's standpoint
article: yes
tags: [blog,how to,tutorial,ros,installation,indigo,ubuntu,14.04,robotics,baxter,simulator]

---

# Contents
{:.no_toc}

* This line will be replaced by the ToC, excluding the "Contents" header
{:toc}

**Disclaimer:** although I've been doing robotics for years, I have **never** used ROS. These are the very first step I made in order to having a working `ros` environment on my laptop. As such, they should be taken as-they-are. They are mainly notes for myself in order to track down what I did and avoid doing the same errors.

This page is going to be about ROS installation. For [a summary about the main ROS concepts and some useful command-line tools, go here]({% post_url 2016-02-06-ROS-concepts %}).

# Installing ROS indigo from sources

Why `ros indigo`? Because it is the same version that has been installed on the [Baxter robot](http://sdk.rethinkrobotics.com/wiki/Main_Page) I am going to use at the [Social Robotics Lab](http://scazlab.yale.edu/).

I decided to install from sources. I am used to that when I was working on [yarp](https://github.com/robotology/yarp), and it is the way to go if you want to have access to the source files and get a better idea of the middleware. I went [here](http://wiki.ros.org/indigo/Installation/Source), and I followed the instructions. Here is a summary of what I did.

## Prerequisites

### Setup `sources.list`
Installing `ros indigo` was not particularly difficult. First thing has been to setup my computer to accept software from `packages.ros.org`. I was lucky that `ros indigo` supports `trusty` (i.e. Ubuntu 14.04). I followed [this page](http://wiki.ros.org/indigo/Installation/Ubuntu#indigo.2BAC8-Installation.2BAC8-Sources.Setup_your_sources.list) (Section 1.2 and 1.3):

~~~bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://pool.sks-keyservers.net --recv-key 0xB01FA116
sudo apt-get update
~~~

### Installing bootstrap dependencies

These tools are used to facilitate the download and management of ROS packages and their dependencies, among other things.

~~~bash
sudo apt-get install python-rosdep python-rosinstall-generator python-wstool python-rosinstall build-essential
~~~

### Initializing `rosdep`

~~~bash
sudo rosdep init
rosdep update
~~~

## Building the `catkin` packages
As far as I understood, `ros` devs have been moving away from `rosbuild` and started to used `catkin`. From [here](http://wiki.ros.org/catkin/conceptual_overview):

  > _"catkin combines CMake macros and Python scripts to provide some functionality on top of CMake's normal workflow. catkin was designed to be more conventional than rosbuild, allowing for better distribution of packages, better cross-compiling support, and better portability. catkin's workflow is very similar to CMake's but adds support for automatic 'find package' infrastructure and building multiple, dependent projects at the same time.
  The name catkin comes from the tail-shaped flower cluster found on willow trees -- a reference to Willow Garage where catkin was created."_

In summary: _welcome to the modern age!_

### Creating a catkin workspace

All of my code is in an aptly-named `code` folder. I put the catkin workspace in there.

~~~bash
cd ~/code/
mkdir ros_catkin_ws
cd ros_catkin_ws/
~~~

I chose a _Desktop-Full Install_: this would install ROS, rqt, rviz, robot-generic libraries, 2D/3D simulators, navigation and 2D/3D perception packages. 

~~~bash
rosinstall_generator desktop_full --rosdistro indigo --deps --wet-only --tar > indigo-desktop-full-wet.rosinstall
wstool init -j8 src indigo-desktop-full-wet.rosinstall
~~~

### Resolving dependencies
Before you can build your catkin workspace, you need to make sure that you have all the required dependencies. They use the `rosdep` tool for this:

~~~bash
rosdep install --from-paths src --ignore-src --rosdistro indigo -y
~~~

This will look at all of the packages in the `src` directory and find all of the dependencies they have. Then it will recursively install the dependencies. 

### Building the catkin Workspace

Once it has completed downloading the packages and resolving the dependencies you are ready to build the catkin packages. We will use the `catkin_make_isolated` command because there are both catkin and plain cmake packages in the base install, when developing on your catkin only workspaces you should use `catkin/commands/catkin_make`.

Invoke `catkin_make_isolated`:

~~~bash
./src/catkin/bin/catkin_make_isolated --install -DCMAKE_BUILD_TYPE=Release
~~~

**WARNING:** this took me loong time. I don't really remember how long, but I'd say one hour for the desktop-full install.

Now everything should be set up correctly. It's time to [follow some tutorials](http://wiki.ros.org/ROS/Tutorials).

# Installing and Configuring Your ROS Environment

**LINK:** [http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment](http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment)

## `.bashrc`

Reading here and there, I added this to my `~/.bashrc` file:

~~~bash
# Ros stuff
export ROS_ROOT="~/code/ros_catkin_ws/install_isolated"
export PATH=$ROS_ROOT/bin:$PATH
source $ROS_ROOT/setup.bash
~~~

Otherwise, I would not have been able to do the steps below.

## Create a ROS workspace

Let's create a catkin workspace (as I said, I have everything in my `code` folder):

~~~bash
cd code/
mkdir -p catkin_ws/src
cd catkin_ws/src
catkin_init_workspace 
~~~

Even though the workspace is empty (there are no packages in the `src` folder, just a single `CMakeLists.txt` link) you can still `build` the workspace:
~~~bash
cd ../
catkin_make
~~~

The catkin_make command is a convenience tool for working with catkin workspaces. If you look in your current directory you should now have a `build` and `devel` folder. Inside the `devel` folder you can see that there are now several `setup.*sh` files. Sourcing any of these files will overlay this workspace on top of your environment:

~~~bash
source devel/setup.bash
~~~

To make sure your workspace is properly overlayed by the setup script, make sure `ROS_PACKAGE_PATH` environment variable includes the directory you're in.

~~~bash
[alecive@malakim]$ echo $ROS_PACKAGE_PATH
/home/alecive/code/catkin_ws/src:/home/alecive/code/ros_catkin_ws/install_isolated/share:/home/alecive/code/ros_catkin_ws/install_isolated/stacks
~~~

