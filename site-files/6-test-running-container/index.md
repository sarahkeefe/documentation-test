---
layout: default
title: Test running your container
nav_order: 6
has_children: true
---
# Test running your container

Once you have a usable container image, the next step is to try out a run of your containerized workflow on your test data. 

First you need to set up a run command which will run one instance of your container on your test data.

Instead of jumping right in to run the whole script, it can be useful to try out some sub-steps first to make sure you are setting up your run command correctly, mapping your files to the container correctly, and aware of where files are within your container once it is running.

Once you get to the point where you can run some example commands in your container, then you can set up a command specific to your workflow script. This is likely to require some rounds of trying your run command, finding an error, fixing the error in your container image definition or input files, and rebuilding your container image. 

- [Docker run command details]
- [Apptainer run command details]
- [Run command troubleshooting tips]

----
[Docker run command details]: https://sarahkeefe.github.io/documentation-test/6-test-running-container/docker-run-command
[Apptainer run command details]: https://sarahkeefe.github.io/documentation-test/6-test-running-container/apptainer-run-command
[Run command troubleshooting tips]: https://sarahkeefe.github.io/documentation-test/6-test-running-container/run-command-troubleshooting-tips