

# Step 8: Test an initial build of your container image

Once you have all the steps written out in your container definition file, it is time to try running an initial build of the container image.

## Build a Docker image from a Dockerfile

The basic Docker build command format is as follows:

```
docker build -t [container_tag]:[container_version_number] .
```

This command expects to find a container definition file named Dockerfile and any input files that get used with a "COPY" instruction in the folder you run the command from. When running the build command, include a tag name and version for your image. The Docker tag name is in the format "dockerhubusername/imagename" and the version number can be a number or string.

"dockerhubusername/" is only needed if you are planning to push your image to Docker hub right away. You can always re-tag it later. For now I will use the tag name "container_tutorial:1.0-dev"

Make sure you are in the directory that contains you program files and Dockerfile. For my example I will run this build command:
```
docker build -t container_tutorial:1.0-dev .
```
The build command will look for a file named "Dockerfile" in your current folder. The dot at the end tells Docker to look for your other input files in the current directory- it will expect every file that you copy with a COPY instruction to be located in the folder you run this command from. If neither of those things is true you will get an error and the build won't work.

If you want to run your build command on a Dockerfile with a different filename, for example "Dockerfile_test1", use this format:

```
docker build -t container_tutorial:1.0-dev -f Dockerfile_test1 .
```

More details on the Docker build command can be found here: [TODO GET LINK]

## Build a Singularity image from a Singularity definition file

The basic Singularity build command is in this format:
```
sudo singularity build containername.sif definitionfile.txt
```


For Singularity, you will need to use the --fakeroot flag to perform the build unless you are on a system where you have administrative/sudo permissions.

Here is my example build command with the definition file from this tutorial:
```
sudo singularity build container_tutorial_1_0-dev.sif singularity_with_ubuntu_as_base.txt
```


This will build a singularity container file with the name "container_tutorial_1_0-dev.sif". The last parameter, singularity_recipe.txt, is the filename of your container definition file.

## Troubleshooting issues with the build

Your build may fail on a particular step. The container engine build process will tell you which step it failed on and will most likely show you the most recent commands it has taken that didn't work. Singularity builds will point you towards a log file that might contain more information. Use this info to diagnose what might have gone wrong. Some potential issues might include:
- Problems with a download link for application files coming from the cloud
- issues with package installers for the operating system of your base container that may require package manager-specific cleanup or update command steps before running the package manager install steps.
- Problems installing a particular program like FSL without all dependencies appropriately met within the container (this requires adding build steps to make sure all those dependencies are present before the main program install step)

When you run into issues, modify your container definition file, save it, and then re-attempt the build command you were using until the container image build program can get past that particular step. Continue the troubleshooting and build attempt cycle until you are able to get a final image built.

## Check that your image built correctly

### Docker
Once your build commands complete in Docker, run
`docker image ls`
You should see the tag of the image you built in the list.
If you see a lot of images that have empty tags, these are most likely intermediate images from failed builds. You can run 
`docker system prune`
to clean up some of those intermediate untagged images.

### Singularity
After a successful build in Singularity, you should have a file of .sif format in your build directory. In our build example command the filename would be "container_tutorial_1_0-dev.sif".
