---
layout: default
title: Put your commands in a simple script file
parent: Convert workflow for containerized use
nav_order: 2
---

# Convert your workflow commands into a simple script file.

Next we are going to convert your workflow_commands.txt file into a very basic script. This example will convert it into a shell script using bash shell syntax. 

To make your workflow_commands.txt file into a bash script, add a "shebang" line at the beginning to indicate the script is in the bash scripting language:
```
#!/bin/bash
```

Make sure all comments and text you have in the .txt file that are not performing some kind of command or workflow action are "commented out" by placing a # at the beginning of the line. So if your script has the text

```
running fslroi
```

Before the actual "fslroi" workflow command, update it to a script comment with a #:
```
# running fslroi
```

Another thing that will be useful to do in this step is to add "print statements" using the bash "echo" command so when the script is called via the command line, the user will see some more output saying what step of the workflow is about to happen. In bash, you can add a print statement like this:

```
echo "About to run step 2"
```

That will print the text in the double quotes to the command line when the script gets to that point.

Once you have updated the script to include a shebang line, commented text, and print statements, save it in your containerization_tutorial folder with the name workflow_script.sh. 

Then go into that folder
```
cd containerization_tutorial
```

clear your output folder from your previous test
```
rm -r output/*
```

and then run your single workflow script via the command line:
```
./workflow_script.sh
```

If you are creating your script on a Windows computer and then running it via a Linux command line, there is a chance you might need to convert the script file's line endings from Windows format to Unix format. This can be done either by installing and using the Unix "dos2unix" program, or with this "sed" command:

```
sed -i.bak 's/\r$//' workflow_script.sh
```

That command will create a backup file but will update your main workflow_script.sh file to be usable with Unix systems.

An example of our updated script file for this step is at step3-initial_workflow_script.sh. This update includes some cleaned up comments and printout statements for each step in the workflow.

Once you run your workflow_script.sh file in the command line, check the output that printed to the command line to make sure none of the workflow steps gave an error, and check the output folder to see if the output files are exactly as they were after your previous line-by-line testing.
