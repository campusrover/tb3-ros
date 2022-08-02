# tb3-ros

**This image contains some customizations for class Cosi119a@brandeis**

## Intro

This is a docker image to allow you to run ROS and related applications through your browser. The following is installed:

* ROS Melodic
* VSCode
* NoVNC desktop
* Turtlebot3 packages
* prrexamples: examples from the book Programming Robotis with Ros
* Here are some handy commands for later: https://campus-rover.gitbook.io/lab-notebook/ros-tips/handy-commands


## Versions and tags in Docker Hub

When you are experimenting with docker file, name tag build as dev-n. Once you are happy with a version and you want to release it then tag the build as vn.n. This seems like extra work but my experience is that you have a hard time keeping things straight if you push changed versions with the same tag. It's a nusiance but be diligent about the version numbers.

There are two stages. Stage 1 is in the directory cosi119-ubuntu-desktop-lxde-vnc-ros and stage 2 is in the directory tb3-ros. It seemed to me that Stage 1 changed very rarely and might be used as a base for other docker images. Stage 2 has more detailed stuff which you probably have to add to from time to time.

Sometimes it seems to me that it matters what kind of computer you use for docker build. I am not sure but I suspected that I got different results on an Intel Mac vs. a M2 Mac. Not sure but I mention it as a hint.

## Building

**Stage 1**

$ cd ubuntu-desktop-lxde-vnc-ros
$ docker build -t cosi119/ubuntu-desktop-lxde-vnc-ros:devel-xxx
$ docker push cosi119/ubuntu-desktop-lxde-vnc-ros:devel-xxx

**Stage 2**

$ cd tb3-ros
$ docker build -t cosi119/tb3-ros:devel-xxx
$ docker push cosi119/tb3-ros:devel-xxx


## Standalone image

**Tested on Windows, Mac, Ubuntu**

`tb3-ros` can be started as on a local docker installation.

See [campusrover/clouddesktop-docker](https://github.com/campusrover/clouddesktop-docker).
