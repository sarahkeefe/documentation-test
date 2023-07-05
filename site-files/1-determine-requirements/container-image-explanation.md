---
layout: default
title: Container image overview
parent: Determine container requirements
nav_order: 2
---

# Explanation: container image vs. container definition file

The process of containerizing your workflow can be referred to as "building a container image". A "container image" differs from a "container", and both differ from a "container definition file". 
A "container definition file" is used to build a container image. In Docker, the definition file can be in Dockerfile format to build using the "docker build" command, or in YAML format to build using "docker-compose". In Singularity, a definition file or "def file" is in the singularity def file format and is built using "singularity build". 

In either platform, the container definition file contains instructions on how to build a container image that contains the programs and files you need to run your workflow. Instructions include specification of the operating system version to use in the container image, commands to download and install software and libraries that you need, commands to copy in your own custom files, and definitions of any environment variables that you want to be set any time your container image is run as a container.

When you share your container image with others, you can technically send them a set of your input files along with your container definition text file, and give them instructions on how to build it. But if your definition file steps include downloading files from the internet to install in your container, there is a chance that install steps may fail if URLs change. For maximum reproducibility, you would want to build your container image yourself, and then share the image itself with others who are using the same platform. 

