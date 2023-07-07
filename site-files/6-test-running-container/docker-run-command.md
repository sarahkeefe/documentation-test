---
layout: default
title: Docker run command setup
parent: Test running your container
nav_order: 1
---

# Set up a Docker run command to run your script on some data

## Docker run command overview

A very basic Docker run command looks like this:
```
docker run -t yourimagetag:yourimageversion
```

the -t parameter when using "docker run" is used to specify the tag and version of the image you want to run a container of. For testing your container, you should use the tag and version that you specified in the "docker build" command. 
In the example build, the tag and version we used was `container_tutorial:1.0-dev`, so your command would look more like this:
```
docker run -t container_tutorial:1.0-dev
```

Running that command will start up a container based on your image tagged `container_tutorial:1.0-dev`. You'll see a command prompt with a different label that indicates you are inside a running container from your image.

[ INSERT IMAGE OF COMMAND PROMPT WITHIN CONTAINER ]

You are inside an instance of your container! You are in the operating system of your base container, and all the instructions you entered in your Dockerfile have been run. You can run standard operating system commands from here.

However, in this tutorial, we haven't added what is called an entrypoint to our container build Dockerfile[^1]. This means that no commands will get run by default when you start an instance of your container. So in this case, starting a container instance with your `run` command will just start a container from it with no commands sent to it. This means the container will just keep running. You can see that by typing

```
docker ps
```

which will show the list of currently running containers on your system. You should see a single instance of your container image running. 

[ INSERT IMAGE OF CONTAINER RUNNING ENDLESSLY ]

When you run a container from an image, Docker gives the container a name[^2] that you can then use to terminate the container with the command

```
docker kill CONTAINER_NAME
```

In this case, I would terminate my endless container with
```
docker kill [INSERT ACTUAL CONTAINER NAME]
```

While it would probably be more straightforward to set an entrypoint in the container, for testing and tutorial purposes here we will tack commands on to the container run command, like this: 

```
docker run -t container_tutorial:1.0-dev COMMAND_TO_RUN_IN_CONTAINER
```

The text `COMMAND_TO_RUN_IN_CONTAINER` should be replaced with a command-line command. This can be pretty much any command that you would be able to run in the operating system of your base container. Eventually we'll add the workflow command onto this, but for now we will use some simpler examples.

## Run a command in your container: List files within the container

As a first example command, just to show that you can run operating system commands within your container, try listing files in the container by sending in the `ls` command. Using our example build tag from earlier, and the command "ls", our run command will look like this: 

```
docker run -t container_tutorial:1.0-dev ls
```

This will show you some output 





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

----

[^1]: [More details on Docker entrypoint setup within a Dockerfile can be found in the Dockerfile reference guide.](https://docs.docker.com/engine/reference/builder/#cmd).
[^2]: [Very charmingly named as an adjective plus a scientist.](https://github.com/moby/moby/blob/master/pkg/namesgenerator/names-generator.go).