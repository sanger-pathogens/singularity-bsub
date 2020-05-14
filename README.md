# singularity-bsub

Provides wrapper scripts for executing LSF commands from within a Singularity container.
The bsub script will bsub a given command using a specified Singularity image.

[![Build Status](https://travis-ci.org/sanger-pathogens/singularity-bsub.svg?branch=master)](https://travis-ci.org/sanger-pathogens/singularity-bsub)

[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-brightgreen.svg)](https://github.com/sanger-pathogens/singularity-bsub/blob/master/LICENSE)

## Requirements

Use of bsub requires the following environment variables to be set:

<b>BSUB_ENVIRONMENT_PROFILES</b> - a comma separated list of full paths to profile
                                   files that should be executed before running the
                                   Singularity command. This is used to set up the
                                   environment in the bsub.

<b>BSUB_SINGULARITY_EXEC</b> - Singularity exe path

<b>CURRENT_SINGULARITY_IMAGE</b> - the Singularity image to be run via bsub (full path)

<b>LSF_BIN_PATH</b> - the full path to the LSF bin directory

<b>LSF_ETC_PATH</b> - the full path to the LSF etc directory

bjobs just needs the two LSF variables.

The wrapper scripts should be built into your Singularity image and
placed at the front of the PATH variable.

Compatible with LSF 10.1.

## Examples

### Variables

	BSUB_ENVIRONMENT_PROFILES="/path/to/my/profile1.rc,/path/to/my/profile2.rc"
	BSUB_SINGULARITY_EXEC="/bin/singularity"
	CURRENT_SINGULARITY_IMAGE="/software/myimage.img"
	LSF_BIN_PATH="/usr/local/lsf/bin"
	LSF_BIN_PATH="/usr/local/lsf/etc"

### bsub (called from Singularity container)

	PATH=/singularity-bsub:${PATH}
	bsub -o job.o -e job.e -R "select[mem>1000] rusage[mem=1000]" -M1000 myprog

Where myprog is a program provided by myimage.img.

## License

singularity-bsub is free software, licensed under [GPLv3](https://github.com/sanger-pathogens/singularity-bsub/blob/master/LICENSE).

