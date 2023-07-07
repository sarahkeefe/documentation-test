---
layout: default
title: Test running your container
nav_order: 6
has_children: true
---

# Test running your container

Once you have a usable container image, the next step is to try out a run of your containerized workflow on your test data. 

First you will need to set up a run command which will run one instance of your container on your test data.

Instead of jumping right in to set up a run command to run your custom workflow script, this tutorial will go over some example run commands first to demonstrate where files are within your running container, setting up the command to send to the container, and mapping your files to the container correctly.

Once you get to the point where you can run some example commands in your container, then you can set up a command specific to your workflow script. This is likely to require some rounds of trying your run command, finding an error, fixing the error in your container image definition or input files, and rebuilding your container image. 

- [Docker run command details]
- [Apptainer run command details]
- [Run command troubleshooting tips]

----
[Docker run command details]: https://sarahkeefe.github.io/documentation-test/6-test-running-container/docker-run-command
[Apptainer run command details]: https://sarahkeefe.github.io/documentation-test/6-test-running-container/apptainer-run-command
[Run command troubleshooting tips]: https://sarahkeefe.github.io/documentation-test/6-test-running-container/run-command-troubleshooting-tips