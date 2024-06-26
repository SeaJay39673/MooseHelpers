# Description:

This repository is for managing helper functions for MOOSE in a Linux environment.

This repo is intended for personal use.

# DISCLAIMER
    Running setup and uninstall scripts will require sudo privileges.
    These scripts will create/remove scripts from your /bin directory and paths from your ~/bashrc file.
    Use at your own discretion.
# Setup:
    To setup and make the helpers available to you, clone this repository and run:
```Bash
./<path-to-repository>/SetupScripts
```
    This script will run the scripts in the setup directory first. 
    The setup scripts create new scripts within the scripts directory.
    Then, this script will copy the script files into your /bin/ directory.
    Finally, the paths to the newly copied files are updated in the environment variables.
## Note:
    Rerunning SetupScripts will rebuild and recopy the files to /bin/,
    but will not update the $PATH environment variables if done once before.

# Uninstall:
    To uninstall the scripts, simply run:
```Bash
./<path-to-repository>/UninstallScripts
```
    This will remove the paths appended to ~/.bashrc and the script files from the /bin/ directory.
    
# Helpers:

## SetupScripts
    This script will copy the following script files to the users /bin/ directory.
    The ~/.bashrc file will be modified to update the $PATH variable to include these files from the /bin/ directory.
    This allows the user to simply reference the name of the script, and not have to specify the path to the script.

## peacock:
    This is a wrapper script to make use of peacock from the moose directory. Use this wrapper to open output files.
### Examples:
```Bash
#Ex 1:
peacock <path-to-out-file>
```

## Alert:
    The Alert helper will notify the user when a command has finished. 
    This occurs through both a sound and (optionally) a popup.
    The popup will tell the user whether the command failed or was successful.
    You can also specify to only display a popup on failure with the "-x" flag.
### Examples
```Bash
#Ex 1:
Alert echo test

#Ex 2:
Alert make -j 6

#Ex 3 (with window):
Alert -w make -j 6

#Ex 4 (Display only on failure):
Alert -w -x echow Test
```

## Run:
    The Run helper increases ease of use for running moose applications.
    The Run helper takes in the following inputs:
    Optional:
        -c (Caffeinate flag, use caffeinate to keep machine awake when running process)
        -a (Alert command, will use the Alert helper)
        -w (Window flag, toggles Alert window on, will use -a implicitly if not specified)
        -n (number of cores, will use mpiexec with the number specified)
        -t (number of threads, used in the opt file directly)
        -p (path, manually specify where the application opt file is)
        -v (View result in peacock, will not display Alert window if command ran successfully)
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
Run -w -n 6 -p ../project-opt -i input.i

#Ex 4 (run in parallel with threads)
Run -n 6 -t 2 -i input.i

#Ex 5 (Run and view in peacock)
Run -v -i input.i

#Ex 6 (Run with caffeinate, Alert window, parallel with threads, and view in peacock)
Run -c -w -v -n 6 -t 2 -i input.i
```