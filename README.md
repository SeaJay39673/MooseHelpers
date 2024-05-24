# Description:

This repository is for managing helper functions for MOOSE.

This repo is intended for personal use.

# Setup:
    To setup and make the helpers available to you, clone this repository and run:
```Bash
./<path-to-repository>/scripts/SetupScripts
```
    This function will copy the script files into your /bin/ directory and add the /bin/ paths to the $PATH environment variable in your ~/.bashrc file.
## Note:
    Rerunning SetupScripts will recopy the files to /bin/, but will not update the $PATH variable in ~./bashrc if done once before.

# Helpers:

## SetupScripts
    This script will copy the following script files to the users /bin/ directory. The ~/.bashrc will be modified to update the $PATH variable to include the path to the scripts newly copied into /bin/.
    This allows the user to simply reference the name of the script, and not have to specify the path to the script.

## Alert:
    The Alert helper will notify the user when a command has finished. 
    This occurs through both a sound and (optionally) a popup. The popup will tell the user whether the command failed or was successful.
### Examples
```Bash
#Ex 1:
Alert echo test

#Ex 2:
Alert make -j 6

#Ex 3 (with window):
Alert -w make -j 6
```

## Run:
    The Run helper increases ease of use for running moose applications.
    The Run helper takes in the following inputs:
    Optional:
        -a (Alert command, will use the Alert helper)
        -w (Window flag, toggles Alert window on)
        -n (number of cores, will use mpiexec with the number specified)
        -t (number of threads, used in the opt file directly)
        -p (path, manually specify where the application opt file is)
    Required:
        -i <path-to-input-file>
*Note: if the current directory is one lower than the \<path-to-opt\> file, specifying path is not required*

### Examples:
```Bash
#Ex 1:
Run -i input.i

#Ex 2 (Alert and run in parallel):
Run -a -n 6 -i input.i

#Ex 3 (Alert window, run in parallel, and specify path):
Run -a -w -n 6 -p ../project-opt -i input.i

#Ex 4 (run in parallel with threads)
Run -n 6 -t 2 -i input.i
```