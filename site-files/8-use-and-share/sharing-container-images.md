---
layout: default
title: Sharing container images
parent: Use and share your container
nav_order: 2
---

# Sharing container images

When you share your container image with others, you can technically send them a set of your input files along with your container definition text file, and give them instructions on how to use `docker build` or `apptainer build` to build it. But if your definition file steps include downloading files from the internet to install in your container, there is a chance that install steps may fail if URLs change. For maximum reproducibility, you would want to build your container image yourself, and then share the image itself with others who are using the same platform. 

