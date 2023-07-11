---
layout: default
title: Choosing Docker or Singularity/Apptainer
parent: Introduction
nav_order: 1
---

# Choosing Docker vs. Apptainer

This tutorial will provide details on converting a neuroimaging workflow for containerization using either [Docker] or [Singularity/Apptainer]. You'll need to decide which platform to start with for containerization.

## High-performace compute systems

Apptainer is frequently used on shared high-performance computing systems so may be best if you are are planning to use a high-performance compute cluster for work on large datasets that require a lot of resources.

## Security and permissions concerns

Your institution may recommend or require a particular platform for security reasons. 

Some IT departments may be hesitant to provide users with access to a shared Docker server setup. 

Docker requires a process called the Docker daemon to run in the background. That process requires root privileges for basic tasks like building images and running containers. Users must have permission to run Docker commands so there is potential for exploit risk if users are given Docker command access.

Apptainer requires root privileges to build an initial image, but once an image is built, users can run containers from built images without requiring special privileges or permissions. However, if you are using a machine where you do not have admin privileges, you have a couple of options. 
- You can build your Singularity container image on a different computer where you have admin permissions, and copy the resulting image file onto the system you need to run it on. 
- You can ask your system administrator about getting permissions to use Apptainer's "fakeroot" feature. This feature provides a user with only the privileges they need to build the image.

If you have admin/root privileges on your computer and have installed Apptainer or Docker yourself, then you most likely won't need to worry about issues with permissions. You would be able to build Docker images using "docker build" or build Apptainer images using "sudo" before your "singularity build" command.

## Disk drive space

Apptainer and Docker container builds will take up varying amounts of space depending on the size of the container images you have on your system, created either from pulling existing ones or building new ones.

For an example image size, the official `freesurfer/freesurfer:7.3.2` FreeSurfer Docker image takes about 15GB of space. A default Ubuntu base image is around 70MB, and you would install any programs you need on top of that size. 

Images are mounted virtually when a container is started, and an additional layer added to store any changes to the container as it runs. So if you pull a FreeSurfer container image and launch 5 FreeSurfer containers from it, the 15GB space would apply only once for the single image. Any new data you are generating with each of those containers would get added to the additional storage layer and add to your total space used. 

Where Docker images are stored is dependent on the administrator's configuration of the Docker storage driver.
Apptainer images are stored as .sif format files in your local folders. Apptainer can be configured to use a [cache directory] where you specify a location where intermediate container image build files are stored.

----

[Docker]: https://docs.docker.com/get-started/
[Singularity/Apptainer]: https://apptainer.org/docs/user/latest/

[cache directory]: https://apptainer.org/docs/user/main/build_env.html#cache-folders