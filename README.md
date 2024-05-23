# Description:

This repository is for managing helper functions for MOOSE.

This repo is intended for personal use.

# Helpers:

## SetupScripts
    This script will copy the following script files to the users /bin/ directory. The ~/.bashrc will be modified to update the $PATH variable to include the path to the scripts newly copied into /bin/.
    This allows the user to simply reference the name of the script, and not have to specify the path to the script.

## Alert:
    The Alert helper will notify the user when a command has finished. 
    This occurs through both a sound and popup. The popup will tell the user whether the command failed or was successful.
### Examples
```Bash
#Ex 1:
Alert echo test

#Ex 2:
Alert make -j 6
```

## Run:
    The Run helper increases ease of use for running moose applications.
    The Run helper takes in the following inputs:
    Optional:
        -w (Watch command, will use the Alert helper)
        -n (number of threads, will use mpiexec with the number specified)
        -p (path, manually specify where the application opt file is)
    Required:
        <path-to-input-file>
*Note: if the current directory is one lower than the <path-to-opt> file, specifying path is not required*

### Examples:
```Bash
#Ex 1:
Run input.i

#Ex 2 (Alert and run in parallel):
Run -w -n 6 input.i

#Ex 3 (Alert, run in parallel, and specify path):
Run -w -n 6 -p ../project-opt input.i
```