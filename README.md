# singularity-bsub

Provides wrapper scripts for executing LSF commands from within a Singularity container.
The bsub script will bsub a given command using a specified Singularity image.

## Requirements

Use of bsub requires the following environment variables to be set:

<b>BSUB_ENVIRONMENT_PROFILES</b> - a comma separated list of full paths to profile
                                   files that should be executed before running the
                                   Singularity command. This is used to setup the
                                   environment in the bsub.

<b>BSUB_SINGULARITY_EXEC</b> - Singularity exe path

<b>CURRENT_SINGULARITY_IMAGE</b> - the Singularity image to be run via bsub (full path)

<b>LSF_BIN_PATH</b> - the full path to the LSF bin directory

<b>LSF_ETC_PATH</b> - the full path to the LSF etc directory

bjobs just needs the two LSF variables.

The wrapper scripts should be built into your Singularity image and
placed at the front of the PATH variable.

Compatible with LSF 10.1.
