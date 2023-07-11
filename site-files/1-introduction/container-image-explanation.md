---
layout: default
title: Container images and containers
parent: Introduction
nav_order: 2
---

# Container images and containers

The process of containerizing your workflow can be referred to as "building a container image". A "container image" differs from a "container", and both differ from a "container definition file". 

## Container image definition file

A "container definition file" is a text file used to build a container image. 

In Docker, the definition file can be in `Dockerfile` for use with the `docker build` command, or in YML/.yml format for use with `docker-compose`. 

In Apptainer, a definition file or "def file" is in the Apptainer def file format.

In either platform, the container definition file contains instructions on how to build a container image that contains the programs and files you need to run your workflow. Instructions include specification of the operating system version to use in the container image, commands to download and install software and libraries that you need, commands to copy in your own custom files, and definitions of any environment variables that you want to be set any time your container image is run as a container.

## Container image

A container image is what gets created when you run a container platform build command with your container image definition file as input. It's like a template for creating new processes, or containers, exactly to your specifications.

In Docker, a definition file in `Dockerfile` format is built using the `docker build` command, and a definition file in `.yml` format is built using `docker-compose`. In Apptainer an image is built using `apptainer build`. 

When you run a build command, an image file gets created in a location dependent on your platform choice and configuration options. You can then use the image file to run containers.

## Containers

A container is a process created from a container image. In Docker you would run a container from an image with `docker run` and in Apptainer you would use `apptainer exec`. 

When you run one of these "run commands" using the name of your image as input, the containerization platform will whatever the image you specify to create a new container from it. 

The run command can run an image interactively, so you can go in and use it as a virtual command-line system with your software installed. Run commands can also incorporate specific sub-commands that you want to automatically run in a new container built with your image. 

The second way is what this tutorial will use for setting up a custom workflow:
- First you will set up a custom script for your workflow actions
- Then you will build your container image
- Then you will set up a run command to use your container image to create a new container and send it a command to perform your actions

