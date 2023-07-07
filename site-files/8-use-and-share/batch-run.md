---
layout: default
title: Batch running containers
parent: Use and share your container
nav_order: 1
---

# Batch running containers from your container image

## Running a "batch" of containers

Example batch script where you provide a list of inputs via CSV file and send the inputs to your run command.

Example takes a CSV file as input and expects to find your files in the locations provided
Incorporate your run command in the batch script template but replace your specific values with the values from the CSV file.

## Considerations

Be careful when running the script locally and make sure you don't run too many containers for your system to handle.

If you are running on a high-performance computing system that uses SLURM
