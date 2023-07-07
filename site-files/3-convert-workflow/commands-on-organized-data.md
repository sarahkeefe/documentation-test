---
layout: default
title: Run your workflow on organized data
parent: Convert workflow for containerized use
nav_order: 1
---

# Set up your workflow commands to run on a folder structure containing organized data.

## Organize your input data and create an output folder.

Set up a folder structure with example input data and test running your workflow's commands in order on the organized files.
Here is the folder structure that this example will use. This expects that you will have 3 folders in your working directory: "freesurfers" containing FreeSurfer output folders, "scans" containing folders of imaging scan files for each scan session (in this case downloaded from OASIS-3 in BIDS format), and an empty directory called "output" for your output to be saved into. You can adjust this to be more specific to how your data is stored.

Here is an example folder tree of the folder and file organization this tutorial will use. 

```
├── containerization_tutorial (A folder you created for this project)
    ├── 1-command_list.sh
    ├── 2-hardcoded_simple.sh
    ├── 3-generic_inputs.sh
    ├── freesurfers (folder)
    │    └── OAS30001_MR_d3132 (FreeSurfer subject folder for OASIS scan session)
    │        ├── label (standard FreeSurfer output sub-folder with its normal FS output)
    │        ├── mri (standard FreeSurfer output sub-folder with its normal FS output)
    │        ├── scripts (standard FreeSurfer output sub-folder with its normal FS output)
    │        ├── stats (standard FreeSurfer output sub-folder with its normal FS output)
    │        ├── surf (standard FreeSurfer output sub-folder with its normal FS output)
    │        └── tmp (standard FreeSurfer output sub-folder with its normal FS output)
    ├── output (empty folder)
    └── scans (folder)
        └── OAS30001_MR_d3132 (folder containing scan subfolders for this OASIS scan session)
            └── dwi1 (folder for scan ID="dwi1" for session "OAS30001_MR_d3132")
                ├── sub-OAS30001_sess-d3132_run-01_dwi.nii.gz (NIFTI file for scan dwi1)
                ├── sub-OAS30001_sess-d3132_run-01_dwi.bvec (bvec file for scan dwi1)
                ├── sub-OAS30001_sess-d3132_run-01_dwi.bval (bval file for scan dwi1)
                └── sub-OAS30001_sess-d3132_run-01_dwi.json (BIDS .json file for scan dwi1)
```

You can have multiple FreeSurfer output folders in the "freesurfers" directory, and you can have multiple scan session folders in the "scans" directory, and more scan type folders in the scans/session directory (e.g. have an "anat1" or "dwi2" scan in scans/OAS30001_MR_d3132). But for simplicity in this tutorial this tree only shows the data we will be using.

## Adapt the first command to work with your organized input data and output folder.

Access your folder via the command line. The command below will be different for you based on where your folder is located in your file system.

```
cd containerization_tutorial
```

In workflow_commands.txt file, update the first command in your workflow so it can find the data files (scans and FreeSurfer) based on how you just organized it. Set up your command as though it will be run from within the "containerization_tutorial" folder. Use the relative paths to each file in the organized data subfolders relative to your location in "containerization_tutorial". For example, if you are trying to use the sub-OAS30001_sess-d3132_run-01_dwi.nii.gz file with your command, the relative path to that file from within the containerization_tutorial folder would be

```
scans/OAS30001_MR_d3132/dwi1/sub-OAS30001_sess-d3132_run-01_dwi.nii.gz
```

Since that file is located in the "scans" folder tree within containerization_tutorial.

When your script creates output files, change the output filenames in your command steps to make sure each file gets saved to the empty "output" folder that you created in "containerization_tutorial". For example, if you are creating a file called nodif.nii.gz, the output file path should be

```
output/nodif.nii.gz
```

In this tutorial I am going to suggest giving any output files you create meaningful names that incorporate the label of the scan session you are using. This will reduce any confusion of having multiple output files of the same name and not knowing which session they belong to. We will also be making sure that separate sessions have different output folders, but this is an additional data organization measure I like to take.

So for example, when saving your nodif.nii.gz file to the output folder, incorporate the scan session label like this:

``
output/OAS30001_MR_d3132_nodif.nii.gz
``

Update all references to the input and output files in your first workflow_commands.txt. Below is an example of how it is done for our initial workflow_commands0.txt file.

For our first command in our workflow_commands.txt:

```
fslroi dwi.nii.gz nodif.nii.gz 0 1
```

Since the command runs on our DTI scan file, and we want the output to go into the output folder and be named something meaningful for our particular scan session, the updated command would be:

```
fslroi scans/OAS30001_MR_d3132/dwi1/sub-OAS30001_sess-d3132_run-01_dwi.nii.gz output/OAS30001_MR_d3132_nodif.nii.gz 0 1
```

Once you have your first command updated in your .txt file, return to the command line and ensure that your current working directory is "containerization_tutorial":

```
pwd
```

Then copy the exact command from your text file, and paste it into the command line, and press Enter. 

If you set it up correctly, the first command in your workflow should use the correct files from your file structure and place any output files in the output folder. Ensure that this works the way you expected it to and places the correctly named files in the output folder rather than modifying your input data directly. If you run into any issues, delete everything from the output folder, make any changes to the command and re-try the command until it works as expected.

## Adapt the second command to work with the output of the first command.

Once you have the first command successfully updated to work with the organized file structure, move on to the next command in your text file. Adjust the next command so it uses the file structure and file naming from the output of your first command. If you saved files to the output folder with the first command and then need to use those files as input for the next command, update the file paths in your second command to reflect that.

Here is our second command in our example workflow:

```
bet nodif.nii.gz nodif_brain.nii.gz -f 0.25 -g 0 -m
```

This is running FSL BET on the nodif.nii.gz output file from the previous step.

The updated version of our first command saved our nodif output file saved to "output/OAS30001_MR_d3132_nodif.nii.gz". So we want to update our second (bet) command to use the nodif file where we saved it. We also want to save the output file in the output folder as well so we don't add new files to our source data. We will update our second command like this:

```
bet output/OAS30001_MR_d3132_nodif.nii.gz output/OAS30001_MR_d3132_nodif_brain.nii.gz -f 0.25 -g 0 -m
```

After updating the second command, test it as you did with the previous one. If your second command accidentally removes or modifies files from the previous command, remove everything from your output folder and restart the workflow test: Run the first command on the original output data, then re-try testing the second command with those output files. If your second command goes wrong, re-set back to what the file output was after your first command and then re-try the second command. When command 2 correctly generates the files and sends the output to the correct place, save the final updated command in your workflow_commands.txt file. Then move on to command 3 and perform the same modification, testing, and troubleshooting steps.


## Update the remaining steps of your workflow to run in with the output from the prior step.

Continue to update the rest of your workflow commands in workflow_commands.txt in this way, with each step using the data from the subsequent step, putting any new data in the output folder rather than modifying or adding to your source data folders, and naming the output files in a meaningful way. Save your changes to workflow_commands.txt as you go along. 

As you test, make sure the commands are being run in order without any manual intervention between the steps (like manual file copying or moving by a human). If you need to add in any extra steps such as copying files, include those steps as commands to be run as part of the workflow. For example, if you need to copy a file to another filename between workflow steps, include a "cp" command in your workflow where that needs to be done.


## Re-set your output directory and run a single test of all steps in order.

When you have worked through testing and updating each command in workflow_commands.txt and expect that each command will work with the previous command's output, do a final test to be sure. Remove everything in the output folder:

```
rm -r output/*
```

Then run each line from your workflow_commands.txt file and ensure you can run the lines in order with no intervention.

When you are done, you should be able to:
- Start from your containerization_tutorial directory
- Start with only the source files in their organized structure 
- Start with an empty output folder
- Run each command in workflow_commands.txt in the command line one-by-one, exactly as you have it saved, and get to the next step without needing to do any manual file changes
- Have generated files from your entire workflow after you have run all the commands in workflow_commands.txt.

The files in the "output" folder should be what you would expect to get when you run your workflow.
Once you have this working, move on to the next step.

The updated workflow_commands.txt file after this step is step2-workflow_commands_organized.txt.

