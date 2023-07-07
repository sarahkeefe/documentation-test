---
title: Containerization Tutorial Home
layout: home
nav_order: 1
---

# Neuroimaging Containerization Tutorial Documentation

This is the main page for the documentation of "Containerizing neuroimaging workflows for scalable and reproducible analyses". This is part of a poster presentation[^1] shown at the Alzheimer's Association International Conference in July 2023.

## Documentation overview

If you are aiming to follow the process to containerize a neuroimaging workflow you use regularly, it may be helpful to walk through the tutorial steps with the provided scripts. 

The first part of the tutorial, "[Determine requirements for your container]" provides some guidance on decisions to be made when containerizing a workflow.

The second part of the tutorial, "[Convert your workflow for containerized use]"
The [scripts] folder contains 5 files that demonstrate the steps of converting a set of workflow steps to a single versatile script that can be used within a container. 

The third part, "[Create your container image definition file]" walks you through the steps of setting up a definition file (Dockerfile or Singularity/Apptainer recipe) for the container image you are developing.

The fourth part, "[Build your initial container image]" provides example build commands to use when building an image from your image definition file, and provides guidance on troubleshooting errors and re-building as needed to get to a completed build.

The fifth part, "[Test out running a container from your image]" provides details on how to use `docker run` or `singularity exec` commands to get started running your container, starting with simple commands and working up to running your customized script.

"[Compare your outputs]" provides some tips on checking whether the output files from your initial container run are identical to the results from your initial testing performed with your workflow conversion process.

The final two sections focus on utilizing your container for reproducible research. "[Batch scripting with your container]" provides details and examples of how to run multiple instances of your container at once. "[Share your container image]" gives details on how to share and push your container to the cloud. 

----

[^1]: [Link to poster presentation can be found in the Alzheimer's Association journal publication from AAIC 2023](https://alz.org).

[Determine requirements for your container]: https://sarahkeefe.github.io/documentation-test/1-determine-requirements
[scripts]: https://github.com/sarahkeefe/documentation-test/tree/main/scripts
[Convert your workflow for containerized use]: https://sarahkeefe.github.io/documentation-test/2-convert-workflow
[Create your container image definition file]: https://sarahkeefe.github.io/documentation-test/3-create-definition-file
[Build your initial container image]: https://sarahkeefe.github.io/documentation-test/build-container-image
[Test out running a container from your image]: https://sarahkeefe.github.io/documentation-test/test-running-container
[Compare your outputs]: https://sarahkeefe.github.io/documentation-test/compare-outputs
[Batch scripting with your container]: https://sarahkeefe.github.io/documentation-test/batch-scripting
[Share your container image]: https://sarahkeefe.github.io/documentation-test/share-your-container