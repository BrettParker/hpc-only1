---
title: "Scheduler cheat sheet"
teaching: 0
exercises: 0
questions:
- "Key question"
objectives:
- "First objective."
keypoints:
- "First key point."
---

##Common PBS commands

#!/bin/bash
#PBS -flag
flags   **-M** setting email recipient list
        **-N** specifying job name


PBS_JOBID       Job identifier given by PBS when the job is submitted. Created upon execution
PBS_JOBNAME     Job name given by user. Created upon execution.
PBS_O_WORKDIR   Absolute path to directory where qsub is run. Value taken from user’s submission environment.




* **pbsnodes -a** print node information


cd $PBS_O_WORKDIR
module load R

R CMD BATCH /export/home/<sNumber>/nameOfRFile.R ## the directory path to navigate to the R script to run
results.Rout ## output from the above r script

## Querying once the job has been submitted
* **qsub** submit a job
* **qstat**
* **qdel *jobID*** delete a job that is running on the HPC