---
layout: default
title: Determine the structure of your workflow
parent: Determine container requirements
nav_order: 3
---

# Determine the structure of your workflow

## Gather your list of workflow commands.

Make sure you have the list of commands that you will need to run and determine the order you need to run them in. Determine what your input files are and what output files are expected at the end of your workflow. 

If you are running programs in a program that uses a user interface, such as some FSL programs, use the documentation for that specific program to determine the equivalent commands that do the same task via the text-only command line, and try the command-line commands out to make sure they give the output you expect.

Set up a text file, workflow_commands.txt, to organize your commands and plan what steps you want to do in which order. Here are some example commands you might be running:

fslroi on a DTI scan file called "dwi.nii.gz", creating an output called "nodif.nii.gz"
```
fslroi dwi.nii.gz nodif.nii.gz 0 1
```

FSL Brain Extraction Tool on "nodif.nii.gz"
```
bet nodif.nii.gz nodif_brain.nii.gz -f 0.25 -g 0 -m
```

eddy_correct on the "dwi.nii.gz" scan file
```
eddy_correct dwi.nii.gz eddy_corrected.nii.gz 0
```

dtifit on the eddy_corrected output plus the bet-extracted nodif file, incorporating the bvec and bval information for the original DTI scan.
```
dtifit -k eddy_corrected.nii.gz -m nodif_brain.nii.gz -r dwi.bvec -b dwi.bval -o dtidata.nii.gz
```

It can be helpful to add comments in your workflow_commands.txt file about what each step does. 

## Try out the individual workflow commands in order.

Once you know your workflow and have tried it on some test data to make sure it gives the output you want, then continue to the next step to start testing it in a more structured fashion on some organized data. 

Our example workflow_commands.txt file for this step can be seen in the file step1-workflow_commands_initial.txt.