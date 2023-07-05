---
layout: default
title: Choosing Docker or Singularity
parent: Determine container requirements
nav_order: 1
---

# Deciding between Docker and Singularity

You may be choosing your containerization system based on what your institution recommends or requires. 

Some IT departments may be hesitant to provide users with access to a shared Docker server setup due to security concerns. Docker requires a process to run in the background that requires root privileges for basic tasks like building images and running containers, so there is potential for exploit risks if users are given Docker command access. Because of this, many high performance computing environments prefer Singularity.

Singularity requires root privileges to build an initial image, but once an image is built, users can run containers from built images without requiring special privileges or permissions. However, if you are using a machine where you do not have admin privileges, you have a couple of options. 
- You can build your Singularity container image on a different computer where you have admin permissions, and copy the resulting image file onto the system you need to run it on. 
- You can ask your system administrator about getting permissions to use Singularity's "fakeroot" feature. This feature provides a user with only the privileges they need to build the image.

If you have admin/root privileges on your computer and have installed Singularity or Docker yourself, then you most likely won't need to worry about issues with permissions. You would be able to build Docker images using "docker build" or build Singularity images using "sudo" before your "singularity build" command.