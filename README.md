# tb3-ros

**This image contains some customizations for class Cosi119a@brandeis**

## Intro

This is a docker image to allow you to run ROS and related applications through your browser. The following is installed:

* ROS Melodic
* VSCode
* NoVNC desktop
* Turtlebot3 packages
* prrexamples: examples from the book Programming Robotis with Ros
* Gen5: Assignments for this generation of Cosi119a
* Here are some handy commands for later: https://campus-rover.gitbook.io/lab-notebook/ros-tips/handy-commands


## Building

The Dockerfile will is `built` into a Docker image with this command:

`make build`

Which will create a docker image called `cosi119/tb3-ros:dev`, that is, with tag `dev`. Once you have tested it and decided that it is good to go you will push it to hub.docker.com. I like to keep the :dev tag until I know I have a good one.

`make push`

Which will push the docker image to hub.docker.com. Change the tag at this point to reflect the version history. You can add other tags to describe it further if you like

## Standalone image

**Tested on Windows, Mac, Ubuntu**

`tb3-ros` can be started as on a local docker installation.

See [campusrover/clouddesktop-docker](https://github.com/campusrover/clouddesktop-docker).
