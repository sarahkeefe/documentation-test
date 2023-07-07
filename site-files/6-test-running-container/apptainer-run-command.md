---
layout: default
title: Apptainer run command setup
parent: Test running your container
nav_order: 1
---

# Step 9: Set up a run command to run your script on some data

Once you have a usable container image, you then can set up a run command to run your containerized workflow on your test data. This will most likely require some rounds of testing, rebuilding, and troubleshooting. First you need to set up a run command which will run one instance of your container on your test data. instead of jumping right in to run the whole script, it can be useful to try out some sub-steps first to make sure you are setting up your run command correctly, mapping your files to the container correctly, and aware of where files are within your container once it is running.

## Docker 

### Docker run command overview

The most basic Docker run command looks like this:

`docker run -t yourimagetag:yourimageversion COMMAND_TO_RUN_IN_CONTAINER`

the -t parameter when using "docker run" is used to specify the tag and version of the image you want to run a container of. For testing your container, you should use the tag and version that you specified in the "docker build" command. 
In the example build above, the tag and version we used was container_tutorial:1.0-dev.

The text "COMMAND_TO_RUN_IN_CONTAINER" should be replaced with a command-line command. This can be pretty much any command that you would be able to run in the operating system of your base container. 

There are many other parameters that can be added to the docker run command, but this basic one is fine to get started.

### List files within the container

As a first example command, just to show that you can run operating system commands within your container, try listing files in the container with the `ls` command. Using our example build tag from earlier, and the command "ls", our run command will look like this: 

`docker run -t container_tutorial:1.0-dev ls`





### Show environment variables with env


### Run your script within the container - basic


### Map your volumes to tell your container where your data is


### Set up a run command and run a test
when you need to rerun, remove all files from the output folder so you know where the most recent issue is. OR create a new output directory and update your run command to send the output there. you want to make sure you have a cleaned up environment when troubleshooting so you know exactly where the latest problem might be, and also make sure you don't run certain steps twice on top of each other/on top of existing files.

## Singularity

### Singularity run command basics


### List files within the container


### Show environment variables with env


### Run your script within the container - basic


### Map your volumes to tell your container where your data is


### Set up a run command and run a test
when you need to rerun, remove all files from the output folder so you know where the most recent issue is. OR create a new output directory and update your run command to send the output there. you want to make sure you have a cleaned up environment when troubleshooting so you know exactly where the latest problem might be, and also make sure you don't run certain steps twice on top of each other/on top of existing files.