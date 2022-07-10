# Slurm
## Slurm Scripting

You can find detail decription of the HPC provision and additional instructions at 
[![HPC Services - School of Biosciences](https://github.com/Peter-Kille/slurm_guide/blob/main/docs/lady_bird.jpg?branch=main)](http://hpc.bios.cf.ac.uk/)

Below I will try to cover the following point of good practice when putting a slurm script together

- [Slurm Parameters](https://github.com/Peter-Kille/slurm_guide/blob/main/docs/index.md#slurm-parameters)
- [Sending Slurm Parameters to outfile](https://github.com/Peter-Kille/slurm_guide/blob/main/docs/index.md#slurm-parameters)
- [Ammeding Script to outfile](https://github.com/Peter-Kille/slurm_guide/blob/main/docs/index.md#slurm-parameters)
- [Defining varibles](https://github.com/Peter-Kille/slurm_guide/blob/main/docs/index.md#slurm-parameters)
- [Loops](https://github.com/Peter-Kille/slurm_guide/blob/main/docs/index.md#slurm-parameters)
- [Sending Batches of jobs](https://github.com/Peter-Kille/slurm_guide/blob/main/docs/index.md#slurm-parameters)

## Slurm Parameters

These slurm parameters use the defq queue (partition), 8 cups need for each task (cpus-per-task) and 8Gb RAM per CPU (mem-per-cpu) - this is for for those small task e.g. running fastp.  Often I will not include the email motification functions as this can end up filling up your email.
```
#!/bin/bash
#author: Peter Kille           # script author
#SBATCH --job-name=job_name    # job name that will appear in scheduler
#SBATCH --partition=defq       # the requested queue
#SBATCH --nodes=1              # number of nodes to use
#SBATCH --tasks-per-node=1     # keep this to 1 to send job to one node
#SBATCH --cpus-per-task=8      # CPUs to be used
#SBATCH --mem-per-cpu=8000     # in megabytes, unless unit explicitly stated
#SBATCH --error=%J.err         # redirect stderr to this file
#SBATCH --output=%J.out        # redirect stdout to this file
##SBATCH --mail-user=[insert email address]@Cardiff.ac.uk  # email address used for event notification
##SBATCH --mail-type=end                                   # email on job end
##SBATCH --mail-type=fail                                  # email on job failure
```
These parameters will generate standard output files using the job number with ```.out``` and ```.err``` ammended - thes erae great for trouble shoting.

If you are performing an oppertion that will take substantial RAM e.g. assembly you may wish to define total memory rather than memory per CPU.  For these job replace ```#SBATCH --mem-per-cpu=8000``` for ```#SBATCH --mem=200000```


## Sending Slurm Parameters to outfile
Including echo commands to send the parameters to the ```.out``` file can be extermely useful to know what parameters you were using. N
```
echo "Some Usable Environment Variables:"
echo "================================="
echo "hostname=$(hostname)"
echo \$SLURM_JOB_ID=${SLURM_JOB_ID}
echo \$SLURM_NTASKS=${SLURM_NTASKS}
echo \$SLURM_NTASKS_PER_NODE=${SLURM_NTASKS_PER_NODE}
echo \$SLURM_CPUS_PER_TASK=${SLURM_CPUS_PER_TASK}
echo \$SLURM_JOB_CPUS_PER_NODE=${SLURM_JOB_CPUS_PER_NODE}
echo \$SLURM_MEM_PER_CPU=${SLURM_MEM_PER_CPU}
```
Note that the defined varibles can be used in the script - so if you program allows you to define threads using paramemeter ```-t``` used you can define this by using ```-t  ${SLURM_JOB_CPUS_PER_NODE}```

If you are using a script that defines total memory replace ```echo \$SLURM_MEM_PER_CPU=${SLURM_MEM_PER_CPU}``` with ```echo \$SLURM_MEM_PER_NODE=${SLURM_MEM_PER_NODE}```

## Ammeding Script to outfile

## Defining varibles

## Loops

## Sending Batches of jobs

   [hpc-bios]: <http://hpc.bios.cf.ac.uk/>
 
