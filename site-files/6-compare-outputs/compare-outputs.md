# Step 12: compare the results to your local testing

If your output is quantitative values - check whether they are identical. They may not be identical due to differing systems with certain programs, or differing program versions from your local system to the container. If you expect them to be the same and they are not, then begin to examine the steps that created those values and work backwards to try to determine where the containerized version diverged from your local version. 

If your output is image files - Examine your final outputs and find out whether they look the same
Could use fslmaths subtract and fslstats (give command example) to compare output images and find out if they are identical if you are expecting that your environment and the container environment should be giving identical results. This may not work for some programs or if you are using different versions of programs.

If the output is not as you expect, check the output from the prior command and compare it to your local output from that prior command. Use similar steps - view the images in a viewer like fsleyes or freeview. 
