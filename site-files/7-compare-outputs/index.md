---
layout: default
title: Check container output
nav_order: 8
has_children: false
---

# Check the output of your container

## Getting container logs

As your containerized workflow runs, it will write output to the console displaying its progress. For shorter workflows such as the one demonstrated, it is relatively easy to examine the output just via viewing the console output. For longer workflows you may want to save the logs other ways in order to view them later. 

### Output redirection to log files

You can use command-line tools such as output redirection to send output from your command to a text file for later viewing:
```
docker run -v /home/usr/sarah/containerization_tutorial/scans:/scans -v /home/usr/sarah/containerization_tutorial/freesurfers:/freesurfers -v /home/usr/sarah/container_tutorial/output:/output container_tutorial:1.0-dev /usr/local/bin/run_workflow.sh /scans /freesurfers /output OAS30001_MR_d3132 dwi1 sub-OAS30001_sess-d3132_run-01_dwi.nii.gz sub-OAS30001_sess-d3132_run-01_dwi.bvec sub-OAS30001_sess-d3132_run-01_dwi.bval 0.25 0 > docker_run_command_output_log.txt
```

```
apptainer exec -B /home/sarah/containerization_tutorial/scans:/scans -B /home/sarah/containerization_tutorial/freesurfers:/freesurfers -B /home/sarah/container_tutorial/output:/output container_tutorial_1_0-dev.sif /usr/local/bin/run_workflow.sh /scans /freesurfers /output OAS30001_MR_d3132 dwi1 sub-OAS30001_sess-d3132_run-01_dwi.nii.gz sub-OAS30001_sess-d3132_run-01_dwi.bvec sub-OAS30001_sess-d3132_run-01_dwi.bval 0.25 0 > apptainer_exec_command_output_log.txt
```

### Docker logs by container name

In Docker, you can add on the `-d` option to run the container in the background in "detached mode". Then you can run `docker ps` to get the list of currently running containers, get your container's assigned name, and then use `docker logs` to view the log output.

First run the command and include the `-d` flag, which will free up the command line for you to run other commands:
```
docker run -d -v /home/usr/sarah/containerization_tutorial/scans:/scans -v /home/usr/sarah/containerization_tutorial/freesurfers:/freesurfers -v /home/usr/sarah/container_tutorial/output:/output container_tutorial:1.0-dev /usr/local/bin/run_workflow.sh /scans /freesurfers /output OAS30001_MR_d3132 dwi1 sub-OAS30001_sess-d3132_run-01_dwi.nii.gz sub-OAS30001_sess-d3132_run-01_dwi.bvec sub-OAS30001_sess-d3132_run-01_dwi.bval 0.25 0
```
That will run the container in the background and output a long container ID string that looks like this:

```
83feefeb506439d3e6bec4596489f063c12067663338f75bca281d1959b7db3c
```

You can get the logs of that container ID by running:
```
docker logs 83feefeb506439d3e6bec4596489f063c12067663338f75bca281d1959b7db3c
```

That output will show the entire log so far. You can rerun that command to show the updated logs as the container runs.

While the container is running, you can also get the assigned container name from the current active container list. Get the active container list with:
```
docker ps
```

You'll see your currently running containers and a generated container name:

![docker-detached-container-name](images/docker-detached-container-name.png){:class="img-responsive"}

In this case the container name is ```intelligent_babbage```. You can then use that name as an input to `docker logs`:
```
docker logs intelligent_babbage
```

### Apptainer process management via Unix

Since Apptainer does not use a centralized service to manage running containers, there is no equivalent way to add a detach flag to `apptainer exec` or view logs via an `apptainer` command. Apptainer output and processes can be used and managed by standard Unix process management commands and features. Unix commands that allow the user to view running processes, bring a running process to the foreground and background, and view and save log output, are the Apptainer equivalent of Docker's container process management commands.

## Ensure that your containerized workflow completed

You can determine if a Docker container completes when it disappears from the `docker ps` console output, and when an Apptainer container process has completed in the shell. When your Apptainer or Docker container process ends, examine the log output and determine if there are any noticeable error messages. 

Error messages may not occur at the very end of the log file. The tutorial script did not include built in checks to determine if prior steps' files exist before proceeding, so the script will attempt to run all commands in order regardless of whether the previous command completed successfully. This can mean that commands get run on output that doesn't exist. Check the log and find the end of each output step to determine if the step completed successfully and confirm that all steps in the workflow worked.

If you have a longer workflow, or steps that spit out a lot of output, it can be hard to find where one workflow step ended and the next one began. An enhancement you can make to your run_workflow.sh script can be to output each step to the console and then run it, like this:

```
# Output the name of the step you are running
echo "Running fslroi"

# Create a string variable with the command text and inputs
cmd="fslroi ${scans_dir}/${session_label}/${dti_scan_id}/${dti_scan_filename} ${output_dir}/${session_label}_nodif.nii.gz 0 1"

# Output the full command you are going to run to the console without actually running it yet
echo "Running command:"
echo ${cmd}

# Use the bash "eval" command to run the exact same command
# the "die" command will end the script if this eval step fails.
eval ${cmd} || die "fslroi failed"
```

You should not only check the logs, but make sure that all the files in your `output` folder are the expected size and quantity that you should have as compared to your initial local testing of your workflow script.

Once you are sure all steps ran and you have the correct number of files, then you can compare the container output and local output files directly.

## Compare quantitative values

If your output is quantitative values - check whether they are identical. They may not be identical due to differing systems with certain programs, or differing program versions from your local system to the container. If you expect them to be the same and they are not, then begin to examine the steps that created those values and work backwards to try to determine where the containerized version diverged from your local version. 

## Compare image files

If your output is image files - examine your final outputs and find out whether they look the same visually and quantitatively. You can use an image viewer like `fsleyes` or `freeview` to check your images based on the file type.

The images may not be identical due to differing systems with certain programs, or differing program versions from your local system to the container. If you are expecting identical image outputs, and need to confirm that your local output is identical to your container output, you can compare them quantitatively with `fslmaths`.

Rename your files so you can know where each one came from, since you will be running commands using two files with the same name. First create a difference image of your local output minus your container output:
```
fslmaths OAS30001_MR_d3132_dtidata_FA_local.nii.gz -sub OAS30001_MR_d3132_dtidata_FA_container.nii.gz OAS30001_MR_d3132_dtidata_FA_local_minus_container.nii.gz
```

Use `fslstats` to determine if any data exists in the difference image:
```
fslstats -V OAS30001_MR_d3132_dtidata_FA_local_minus_container.nii.gz
```
If the output of the fslstats -V command is zero, then there is no data in the difference image, which means that the two images that went into the fslmaths command were identical. If the `fslstats` command gives non-zero output, then there is a difference between the two input images. You can view the difference image in an image viewer to see exactly where the images differed which might give some clues about where the discrepancy came from. 

If your comparison output is not what you expect, use similar steps to check each prior command and work backwards until you can find the place where the local and containerized outputs diverged.