---
layout: default
title: Incorporate command-line inputs
parent: Convert workflow for containerized use
nav_order: 5
---

# Update your workflow script to use inputs from the command line.

## Using positional input values in `bash`

Next you will convert each variable in the variables section of your script to be entered as inputs when running the script via the command line. 

We will use `bash` "positional parameters" to do this in a simple way. When we are done, you will run your script by calling the script file name, and then entering each input value in order, separated by a single space.

When you make the next changes, you will be replacing the values you have in your script for any of the variables you created, so it can be helpful to save those values elsewhere, like in another text file, so you know what inputs you used for your tests. You will run the script with those same inputs when you test this change, so you don't want to forget them.

For our example, our variables and their values are:
```
scans_dir="scans"
freesurfers_dir="freesurfers"
output_dir="output"
session_label="OAS30001_MR_d3132"
dti_scan_id="dwi1"
dti_scan_filename="sub-OAS30001_sess-d3132_run-01_dwi.nii.gz"
dti_bvec_filename="sub-OAS30001_sess-d3132_run-01_dwi.bvec"
dti_bval_filename="sub-OAS30001_sess-d3132_run-01_dwi.bval"
fi_threshold_value=0.25
gradient_value=0
```

Bash expects variables with values like `$1` or `${1}` - a dollar sign and a number - to be referring to a position in the list of inputs sent when the script is called. For example, in a command
```
./myscript.sh ABC DEF GHI
``` 
Within the contents of that script file, `$1` or `${1}` refers to the first input to the script, or `ABC`. `$2` or `${2}` refers to the second input, or `DEF`, and `$3` or `${3}` refers to the third input value, `GHI`, and so on. 

## Updating your script to use input values

Open `convert-workflow/step4-script_with_hardcoded_inputs.sh` in your text editor.

For each line in your script where you set a new variable - in our example, the lines above - replace the value in quotes with the numbers 1 through 10, with brackets and a dollar sign to let bash know you are setting each variable to the value of the positional parameter at that number. So our updated variable lines in our script would look like this:

```
scans_dir=${1}
freesurfers_dir=${2}
output_dir=${3}
session_label=${4}
dti_scan_id=${5}
dti_scan_filename=${6}
dti_bvec_filename=${7}
dti_bval_filename=${8}
fi_threshold_value=${9}
gradient_value=${10}
```

When you call your script after this update, the first input you send after the script name will go into the variable "scans_dir", then the next one will go into "freesurfers_dir", and so on. So your script call expects to receive the variables' values in this order:
```
./step4-script_with_hardcoded_inputs.sh scans_dir freesurfers_dir output_dir session_label dti_scan_id dti_scan_filename dti_bvec_filename dti_bval_filename fi_threshold_value gradient_value
```

Save your script file in your `containerization_tutorial` folder with the filename `inputs_workflow.sh`. 

When you test the script after this update, you will send each of your variable values when you run it in the command line like this:
```
./inputs_workflow.sh scans freesurfers output OAS30001_MR_d3132 dwi1 sub-OAS30001_sess-d3132_run-01_dwi.nii.gz sub-OAS30001_sess-d3132_run-01_dwi.bvec sub-OAS30001_sess-d3132_run-01_dwi.bval 0.25 0
```

Set up your new command with the variables as input parameters in a text editor and check it to make sure you have the inputs correct. 

Remove everything from your output folder from the previous test:
```
rm -f output/*
```

Then try running your script with the variables as inputs with the command that was just mentioned:
```
./inputs_workflow.sh scans freesurfers output OAS30001_MR_d3132 dwi1 sub-OAS30001_sess-d3132_run-01_dwi.nii.gz sub-OAS30001_sess-d3132_run-01_dwi.bvec sub-OAS30001_sess-d3132_run-01_dwi.bval 0.25 0
```

Check to make sure the output in the output folder is identical to how it came out in your previous tests.

Once you are able to send inputs to your script and have your workflow run with them, you'll be able to move on to building a container image to include your script in. 

## Organization for the next steps in the tutorial

Before moving to the next steps, in order to keep things organized, set up a new folder in your `containerization_tutorial` folder tree called `container_image_files`:

```
mkdir container_image_files
```

You'll use this `container_image_files` folder to store all the files that will be a part of your container image build.

Copy your finalized script in there with the name `run_workflow.sh`:
```
cp inputs_workflow.sh container_image_files/run_workflow.sh
```

To be sure you are using a workflow script that matches the expected tutorial output, you can instead use the example final script file from this part of the tutorial, `convert-workflow/step5-script_with_cl_inputs.sh`, and copy that file into `container_image_files` with the filename `run_workflow.sh`.

After this section, your folder tree should look something like this:
```
├── containerization_tutorial (A folder you created for this project)
    ├── single_file_workflow.sh
    ├── variables_workflow.sh
    ├── inputs_workflow.sh
    ├── freesurfers (folder)
    │    └── OAS30001_MR_d3132 (FreeSurfer subject folder for OASIS scan session)
    │        ├── label (standard FreeSurfer output sub-folder with its normal FS output)
    │        ├── mri (standard FreeSurfer output sub-folder with its normal FS output)
    │        ├── scripts (standard FreeSurfer output sub-folder with its normal FS output)
    │        ├── stats (standard FreeSurfer output sub-folder with its normal FS output)
    │        ├── surf (standard FreeSurfer output sub-folder with its normal FS output)
    │        └── tmp (standard FreeSurfer output sub-folder with its normal FS output)
    ├── output (empty folder)
    ├── scans (folder)
    │   └── OAS30001_MR_d3132 (folder containing scan subfolders for this OASIS scan session)
    │       └── dwi1 (folder for scan ID="dwi1" for session "OAS30001_MR_d3132")
    │           ├── sub-OAS30001_sess-d3132_run-01_dwi.nii.gz (NIFTI file for scan dwi1)
    │           ├── sub-OAS30001_sess-d3132_run-01_dwi.bvec (bvec file for scan dwi1)
    │           ├── sub-OAS30001_sess-d3132_run-01_dwi.bval (bval file for scan dwi1)
    │           └── sub-OAS30001_sess-d3132_run-01_dwi.json (BIDS .json file for scan dwi1)
    └── container_image_files (folder) 
         └── run_workflow.sh (your final tested workflow script file)
```
