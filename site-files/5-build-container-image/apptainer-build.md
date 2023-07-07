---
layout: default
title: Apptainer build
parent: Build the container image
nav_order: 2
---

# Build an Apptainer image from an Apptainer definition file

## Simple build command format

The basic Apptainer build command is in this format:

```
apptainer build image_filename.sif apptainer_definition_file.txt
```

For Apptainer, you will need to add in the `--fakeroot` flag to perform the build unless you are on a system where you have administrative/sudo permissions.
Here is my example build command with the definition file from this tutorial:

```
apptainer build --fakeroot container_tutorial_1_0-dev.sif apptainer_def.txt
```

For Apptainer it is helpful to set some environment variables to tell the Apptainer engine where to store intermediate and log files. 
- `APPTAINER_CACHEDIR` specifies where cache files should be stored, and should be set to an absolute directory path (The full path to a directory of your choice, starting with `/`). 
- `APPTAINER_TMPDIR` specifies where temporary build files should go and should also be set to an absolute folder path. 
If a build fails, the files stored in these directories can be helpful to refer to when troubleshooting. 

```
export APPTAINER_CACHEDIR=`pwd`/buildcache
export APPTAINER_TMPDIR=/tmp
```

It can also be helpful to add the `--no-cleanup flag` for troubleshooting, although be aware that this will take up more space on your machine.
Here is the 

apptainer build --fakeroot --no-cleanup edi_workflow_1_0-dev apptainer_def_file.txt

This will build an Apptainer container image file with the name "container_tutorial_1_0-dev". The last parameter, apptainer_def_file.txt, is the filename of your container image definition file.

More details on the Apptainer build command can be found in the [Apptainer build command documentation].

## Running the build command

To run your build command, make sure you are located in the directory that contains your container definition file and workflow script file along with any other files that you are copying into your container image. This should be the "containerization_tutorial/container_files" directory. 

From that folder, run your Apptainer build command:

```
apptainer build --fakeroot container_tutorial_1_0-dev apptainer_def_file.txt
```

The Apptainer engine will go through the build steps in your definition file and run them one by one. 

The build might complete successfully and show a success message at the end. 

If the build does not complete, you should see an error message that indicates that the build failed on a particular step. 

## If your build succeeded: Check that your image built correctly

After a successful build in Apptainer, you should have a file of .sif format in your build directory. In our build example command the filename would be "container_tutorial_1_0-dev.sif".

Once your `apptainer build` command completes, list the files in your current directory:

```
ls
```

If your build completed, you will see the filename of the image you built in the list, like this:

[ INSERT IMAGE OF SUCCESSFUL APPTAINER BUILD IN FILE LIST ]

## If your build failed: Troubleshoot, fix, and rebuild

If your build failed, proceed to the [Troubleshooting and rebuilding step] of this tutorial to get some tips on how to investigate build errors and fix them. You will need to make changes to your container image definition file and rerun the build command until you can get a build to complete successfully.

----
[Apptainer build command documentation]: https://apptainer.org/docs/user/latest/build_a_container.html
[Troubleshooting and rebuilding step]: https://sarahkeefe.github.io/documentation-test/5-build-container-image/troubleshooting-and-rebuilding