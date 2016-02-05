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

# Useful Tools

**LINK:** [http://wiki.ros.org/ROS/Tutorials/NavigatingTheFilesystem](http://wiki.ros.org/ROS/Tutorials/NavigatingTheFilesystem)

## Quick Overview of Filesystem Tools

  * Packages: Packages are the software organization unit of ROS code. Each package can contain libraries, executables, scripts, or other artifacts.

  * Manifest (`package.xml`): A manifest is a description of a package. Its serves to define dependencies between packages and to capture meta information about the package like version, maintainer, license, etc... 

## Summary of the things that are going to be shown here

Let's just list some of the commands we've used so far:

 * `rospack = ros+pack(age)` : provides information related to ROS packages
 * `roscd = ros+cd` : changes directory to a ROS package or stack
 * `rosls = ros+ls` : lists files in a ROS package
 * `roscp = ros+cp` : copies files from/to a ROS package
 * `rosmsg = ros+msg` : provides information related to ROS message definitions
 * `rossrv = ros+srv` : provides information related to ROS service definitions
 * `catkin_make` : makes (compiles) a ROS package

### Using rospack

`rospack` allows you to get information about packages. In this tutorial, we are only going to cover the find option, which returns the path to package. 

~~~bash
[alecive@malakim]$ rospack find roscpp
/home/alecive/code/ros_catkin_ws/install_isolated/share/roscpp
~~~

### Using roscd

`roscd` is part of the `rosbash` suite. It allows you to change directory to a package or a stack. Like other ROS tools, it will **only** find ROS packages that are within the directories listed in your `ROS_PACKAGE_PATH`.

~~~bash
(~) () 
[alecive@malakim]$ roscd roscpp

(~/code/ros_catkin_ws/install_isolated/share/roscpp) () 
[alecive@malakim]$ 
~~~

#### What to do if your package is not listed in `roscd`

You need to update the database:

~~~bash
rospack profile
~~~

### Using rosmsg

Example Usage:

~~~bash
rosmsg show beginner_tutorials/Num
~~~

You will see:

~~~bash
    int64 num
~~~

In the previous example, the message type consists of two parts:

 * beginner_tutorials -- the package where the message is defined
 * Num -- The name of the msg Num. 

If you can't remember which Package a msg is in, you can leave out the package name. Try:

~~~bash
rosmsg show Num
~~~

You will see:

~~~bash
    [beginner_tutorials/Num]:
    int64 num
~~~

### Using rossrv

Example Usage:

~~~bash
rossrv show beginner_tutorials/AddTwoInts
~~~

You will see:

~~~
    int64 a
    int64 b
    ---
    int64 sum
~~~

Similar to rosmsg, you can find service files like this without specifying package name:

~~~
rossrv show AddTwoInts
[beginner_tutorials/AddTwoInts]:
int64 a
int64 b
---
int64 sum

[rospy_tutorials/AddTwoInts]:
int64 a
int64 b
---
int64 sum
~~~

# ROS concepts

A summary of what is available [here](http://wiki.ros.org/ROS/Concepts). I will start from [here](http://wiki.ros.org/Nodes).

## Master

The ROS Master provides naming and registration services to the rest of the nodes in the ROS system. It tracks publishers and subscribers to topics as well as services. The role of the Master is to enable individual ROS nodes to locate one another. Once these nodes have located each other they communicate with each other peer-to-peer.

The Master also provides the Parameter Server.

The Master is most commonly run using the `roscore` command, which loads the ROS Master along with other essential components. 

## Nodes

A node is a process that performs computation. Nodes are combined together into a graph and communicate with one another using _streaming topics_, _RPC services_, and the _Parameter Server_. These nodes are meant to operate at a fine-grained scale; a robot control system will usually comprise many nodes.

All running nodes have a graph resource name that uniquely identifies them to the rest of the system - e.g. `/hokuyo_node`. Nodes also have a node type, that simplifies the process of referring to a node executable on the fileystem. These node types are package resource names with the name of the node's package and the name of the node executable file. In order to resolve a node type, ROS searches for all executables in the package with the specified name and chooses the first that it finds. As such, you need to be careful and not produce different executables with the same name in the same package.

A ROS node is written with the use of a ROS client library, such as `roscpp` or `rospy`. 

## Topics

Topics are named buses over which nodes exchange messages. Topics have anonymous publish/subscribe semantics, which decouples the production of information from its consumption. In general, nodes are not aware of who they are communicating with. Instead, nodes that are interested in data subscribe to the relevant topic; nodes that generate data publish to the relevant topic. There can be multiple publishers and subscribers to a topic.

Topics are intended for unidirectional, streaming communication. Nodes that need to perform remote procedure calls, i.e. receive a response to a request, should use services instead. There is also the Parameter Server for maintaining small amounts of state. 

Each topic is strongly typed by the ROS message type used to publish to it and nodes can only receive messages with a matching type. The Master does not enforce type consistency among the publishers, but subscribers will not establish message transport unless the types match. Furthermore, all ROS clients check to make sure that an MD5 computed from the msg files match. This check ensures that the ROS Nodes were compiled from consistent code bases. 

## Services

The publish/subscribe model is a very flexible communication paradigm, but its many-to-many one-way transport is not appropriate for RPC request/reply interactions, which are often required in a distributed system. Request/reply is done via a service, which is defined by a pair of messages: one for the request and one for the reply. A providing ROS node offers a service under a string name, and a client calls the service by sending the request message and awaiting the reply. Client libraries usually present this interaction to the programmer as if it were a remote procedure call.

Services are defined using `srv` files, which are compiled into source code by a ROS client library.

A client can make a persistent connection to a service, which enables higher performance at the cost of less robustness to service provider changes. 

## Messages

Nodes communicate with each other by publishing messages to topics. A message is a simple data structure, comprising typed fields. Standard primitive types (integer, floating point, boolean, etc.) are supported, as are arrays of primitive types. Messages can include arbitrarily nested structures and arrays (much like C structs).
Nodes can also exchange a request and response message as part of a ROS service call. These request and response messages are defined in `srv` files. 

Message types use standard ROS naming conventions: `package_name/msg_file_name`. For example, `std_msgs/msg/String.msg` has the message type `std_msgs/String`.

In addition to the message type, messages are versioned by an MD5 sum of the `.msg` file. Nodes can only communicate messages for which both the message type and MD5 sum match. 

### Field types

#### built-in types

| **Primitive Type**  | **Serialization**                 | **C++**           | **Python**      |
|     bool            | unsigned 8-bit int                | uint8_t           | bool            |
|     int8,16,32,64   | signed 8,16,32,64-bit int         | int8,16,32,64_t   | int             |
|    uint8,16,32,64   | unsigned 8,16,32,64-bit int       | uint8,16,32,64_t  | int             |
|     float32         | 32-bit IEEE float                 | float             | float           |
|     float64         | 64-bit IEEE float                 | double            | float           |
|     string          | ascii string                      | std::string       | string          |
|     time            | secs/nsecs unsigned 32-bit ints   | ros::Time         | rospy.Time      |
|     duration        | secs/nsecs  signed 32-bit ints    | ros::Duration     | rospy.Duration  |
  
#### Array Handling

|-------------------+-------------------------+-----------------------------------------------+-------------|
| **Array Type**    | **Serialization**       | **C++**                                       | **Python**  |
|:------------------|:-----------------------:|:---------------------------------------------:|:-----------:|
| fixed-length      | no extra serialization  | 0.11+: boost::array, otherwise: std::vector   | tuple       |
| variable-length   | uint32 length prefix    | std::vector                                   | tuple       |
|-------------------+-------------------------+-----------------------------------------------+-------------|
| uint8[]           | see above               | `std::vector<uint8_t>`                        | string      |
| bool[]            | see above               | see above                                     | list(bool)  |
|-------------------+-------------------------+-----------------------------------------------+-------------|

## `msg` and `srv`

`msg` files are stringored in the `msg` directory of a package, and `srv` files are stored in the `srv` directory.

`msg`s are just simple text files with a field type and field name per line. The field types you can use are:

 * int8, int16, int32, int64 (plus uint*)
 * float32, float64
 * string
 * time, duration
 * other msg files
 * variable-length array[] and fixed-length array[C] 

There is also a special type in ROS: the **header**, which contains a timestamp and coordinate frame information that are commonly used in ROS.
Here is an example of a msg that uses a Header, a string primitive, and two other msgs :

~~~
Header header
string child_frame_id
geometry_msgs/PoseWithCovariance pose
geometry_msgs/TwistWithCovariance twist
~~~

`srv` files are just like `msg` files, except they contain two parts: a request and a response. The two parts are separated by a `---` line. Here is an example of a srv file where A and B are the request, and Sum is the response:

~~~
int64 A
int64 B
---
int64 Sum
~~~

The full specification for the message format is available at the [Message Description Language](http://wiki.ros.org/ROS/Message_Description_Language) page.

If you are building C++ nodes which use your new messages, you will also need to declare a dependency between your node and your message, as described in the [catkin msg/srv build documentation](http://docs.ros.org/hydro/api/catkin/html/howto/format2/building_msgs.html).

### Using msg in your package

We need to make sure that the msg files are turned into source code for C++, Python, and other languages:

 * open `package.xml, and make sure these two lines are in it and uncommented:

~~~xml
<build_depend>message_generation</build_depend>
<run_depend>message_runtime</run_depend>
~~~

 * Add the `message_generation` dependency to the `find_package` call which already exists in your `CMakeLists.txt` so that you can generate messages:
    
~~~
find_package(catkin REQUIRED COMPONENTS
   roscpp
   rospy
   std_msgs
   message_generation
)
~~~
    
 * Make sure you export the message runtime dependency:
    
~~~
catkin_package(
  ...
  CATKIN_DEPENDS message_runtime ...
  ...)
~~~

 * Uncomment the following block of code in your `CMakeLists.txt`, and replace the stand in `Message*.msg` files with your `.msg` file.

~~~
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )
~~~

 * We must ensure the generate_messages() function is called. Uncomment these lines:

~~~
# generate_messages(
#   DEPENDENCIES
#   std_msgs
# )
~~~

### Using srv in your package

Let's start by copying an existing one from another package:

~~~bash
roscp rospy_tutorials AddTwoInts.srv srv/AddTwoInts.srv
~~~

Now we need to make sure that the srv files are turned into source code for C++, Python, and other languages. Do step #1, #2, #3, #5 from previous section, and then:

 * Uncomment the following lines, and replace the placeholder Service*.srv files for your service files:

~~~
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )
~~~

Now you're ready to generate source files from your service definition. If you want to do so right now, skip next sections to Common step for msg and srv.
