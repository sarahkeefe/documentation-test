---
layout: default
title: Choosing a base operating system or base image
parent: Determine container requirements
nav_order: 5
---

# Choosing a base operating system or base image

Once you have determined which platform you want to use, gather the requirements for what programs your workflow will need. In subsequent steps you will be setting up a container definition file that incorporates the programs and scripts your workflow uses, including the script you just tested.

The first step of setting up a container image definition file is to determine what operating system it will use, or a "base image" to add your custom scripts to. When setting up a Docker image definition file, the base image must be an existing Docker image, either stored on Docker Hub or locally built on your computer. For Singularity you can either build on top of existing Singularity images, Docker images, or other sources. A base image can either be a simple image that is just a bare-bones operating system in a Docker container, OR it can be a more complex image that has been built to include more programs, configurations, and features. 

Here are a few considerations when choosing a base image:

Does your workflow output need to match existing processing that has happened on particular machines? Some programs like Freesurfer are unlikely that the results will match exactly across machines, but you can choose a comparable base OS in your container to get as close as possible results to the original you are trying to match. For example, if you are running your local test on a machine that is running Ubuntu 20.04, you may want to use the Ubuntu 20.04 Docker base image for your Dockerfile or Singularity definition file.
(Note that exact replication of output across containerized and non-containerized systems may not be possible. Some programs like FreeSurfer are sensitive to small software differences in operating system and program versions and may not be able to replicate results once containerized.) 

Are you only going to need to install one or two major programs in your container, e.g. FreeSurfer or FSL? One of the programs you need to install in your container might already have an official release container that you can use as your base image. Finding an existing container image to build on top of can save time if installing a particular program has a lot of complex dependencies or configurations. 

Does your script require a specific version of a program or programming language? You can choose a tag for an image based on the version you need. For example, if you need to use version Python 3.7.16 exactly, you can use python:3.7.16 as your base image, or choose a specific version of an image using the tag for the version you want. https://hub.docker.com/_/python/tags

Does the operating system and OS version make a difference in your processing or code? If so, you will want to be sure you use a base image that uses that operating system. Using a base image that was created for a particular program will use the operating system chosen by the developers of the image. For example some of the official "freesurfer/freesurfer" Docker images use CentOS 8 as a base image, so if you need your container to be Ubuntu-based, you will want to use Ubuntu as your base image rather than the pre-build Freesurfer image. 

Docker official images: https://docs.docker.com/docker-hub/official_images/
 https://hub.docker.com/search?image_filter=official&q=&type=image

Singularity library images: https://cloud.sylabs.io/library/library

If you want to try to find an existing base image to build from, you can look for built images for these programs that have been shared. You can look on the Singularity Image Library https://cloud.sylabs.io/library or on Docker Hub https://hub.docker.com to find an official existing container image for a program you need, for example freesurfer, and look at the tags section to choose the tag of the version you want to use, e.g. https://hub.docker.com/r/freesurfer/freesurfer/tags. There is a Singularity Catalog where users can post links to their Github pages that have various Singularity image definition files https://singularityhub.github.io/singularity-catalog/. In that case, you could search for a particular program of a particular version, access the Github page, copy the Singularity definition file and any required included files, and   You can use that container as your base container image and then copy your scripts and any other custom files (including a license file) into your custom container image.

There are other sources of images you can build off of ("bootstrap") with Singularity: https://docs.sylabs.io/guides/3.11/user-guide/definition_files.html#preferred-bootstrap-agents but for simplicity I will focus on building an image from a base operating system image.

# Consider whether you can use Neurodocker to save time

If your workflow uses a set of standard neuroimaging programs you can use the command-line program Neurodocker (https://www.repronim.org/neurodocker) to generate a container image definition file for you to add to. Neurodocker is available as a container image which allows you to run the Neurodocker command-line program on your Docker or Singularity server. More details can be found on their Installation page (https://www.repronim.org/neurodocker/user_guide/installation.html). The concept is that you run the Neurodocker command line program with particular input parameters, and then Neurodocker spits out a container definition file with those specifications. With Neurodocker you specify whether you want a Docker or Singularity definition file, choose a base image, and specify versions of common neuroimaging programs to include in your container. Neurodocker includes the ability to copy in external files like your script, and specify environment variables that you want, so if you are only using programs and versions that Neurodocker offers as options, you could feasibly generate your whole container definition file using Neurodocker! You can see the programs and options available from the command-line interface documentation here: https://www.repronim.org/neurodocker/user_guide/cli.html and examples of definition file generation with common programs here: https://www.repronim.org/neurodocker/user_guide/examples.html.
