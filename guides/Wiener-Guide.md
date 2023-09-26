 

# Guide 

## General Information 

Wiener is named in honor of Norbert Wiener, a mathematician who devised an algorithm to remove noise from a signal or image. The technique became known as "Deconvolution". The alternative name for this supercomputer is the "UQ Deconvolution Facility". 


## Hardware 

Wiener phase 1.0 (gpunode-0-[0-16]):<br> 

2 * NVIDIA Volta V100 with<br> 

- 5120 CUDA cores
- 640 Tensorflow hardware cores 
- 16GB of HBM2 class memory. 


Wiener phase 2.0 (gpunode-1-[0-14]):<br>

4 * NVIDIA Volta V100 SXM2 with<br>

- 5120 CUDA cores
- 640 Tensorflow hardware cores
- 32GB of HBM2 class memory.


All compute nodes have 28 CPU cores and 56 threads (slurm cpus), 384GB of ram (the max quota in jobs per user is 300GB).

## Who has access? 

Wiener is exclusively for accelerator-class (GPU) codes. CPU-only workloads are not permitted on Wiener. CPU-only workloads found running on Wiener will be killed.
Users are required to use their UQ staff ID to apply for access to Wiener. Student accounts are not permitted on Wiener. 

## Connecting 

Set 1 of the [Training resources](https://www.qcif.edu.au/training/hpc-training-resources/) explains how to use Putty to connect to a HPC with the basics found [here](https://youtu.be/oP_5JJrMm1U). To connect to Wiener please use: 


Hostname: wiener.hpc.dc.uq.edu.au <br> 
Port: 22 

For those using command line ssh:<br> 

`ssh wiener.hpc.dc.uq.edu.au`

***Wiener enforces MFA (multi factor authentication).*** 

For UQ users, this will use their DUO MFA that is used for all other access to UQ resources. 

Users will first be asked for their password (or key). After users have entered this, they will see one or more options given. Choose the option you wish to use and type the respective number on the command line. If you have only one option set up, you still need to type “1” and press “enter”. 

After this you will be logged into Wiener. 

## File Systems and Quotas

You have access to a set of locations to store data

* /clusterdata/$USER is your home directory, (5GB only, NO BACKUP)
* /scratch/OrgUnit/ is your scratch space, (2TB, NO BACKUP, suggest you create a /scratch/OrgUnit/$USER folder)
* /afm03/ is the top level directory for locating RDM collections. They are arranged in groups of 1000 collections. eg. /afm03/Q5/Q5002



When you login you will see a summary of your home and scratch allocations.
```
------------------------------------------------------------------------------------------------------------------------------------------
Block Limits                                                                          |File Limits
Filesystem   Fileset    type         blocks      quota      limit   in_doubt    grace |    files   quota    limit in_doubt    grace  Remarks
SCRATCH2     root       USR          419.4M         2T     2.148T          0     none |     1871       0        0        0     none
CLUSTERDATA2 root       USR          1.588G         5G        10G          0     none |    12190       0        0        0     none
------------------------------------------------------------------------------------------------------------------------------------------
```

You can also use this command.
` /usr/lpp/mmfs/bin/mmlsquota -e --block-size=auto SCRATCH2 CLUSTERDATA2`


## File Transfer 

We recommend to use command line `scp` and `sftp`. They are accessible to all users, via a shell for Linux and Mac users and via WSL and `cmd` for Windows users. 

`scp file username@wiener.hpc.dc.uq.edu.au:/path-to-place-for-file/` 

For example 

`scp test.dat username@wiener.hpc.dc.uq.edu.au:/scratch/user-OU/username/` 

will copy the file `test.dat` to the user's scratch directory. 

`sftp username@wiener.hpc.dc.uq.edu.au` 

You will see `sftp>` as prompt once you have logged in. 

`ls` and `cd` work as usual on the Wiener end. Use `lls` to list files on your desktop/laptop and `lcd` to change directories on your desktop/laptop. 

Use `get` to pull files and directories from Wiener to your desktop/laptop and use `put` to move files and directories from your desktop/laptop to Wiener. 

Windows users can also use WinSCP if they require a graphical SFTP client. WinSCP allows the MFA authentication without extra setup. WinSCP also allows multiple files and directories transfer without having to re-enter the MFA passcode. 

## Login node 

Wiener has one login node, wiener.hpc.dc.uq.edu.au. You do *not* need to be on the UQ VPN to access it. 

We ask that users be mindful of the nature of a login node. This single login node is shared by all users accessing and using Wiener. **Do not run computational workloads on the login nodes, please.** Compiling, yes. Assembly of your code, yes. Editing your scripts and moving things around, yes. Submitting your jobs via "sbatch", yes. **Running "jobs" on the login node and not using the SLURM scheduler...no.** 

## Software 

The [training resources](https://www.qcif.edu.au/training/hpc-training-resources/) have a short video on how to use [software modules](https://youtu.be/AN0zqXj06N4) to load installed software on HPC. 

The basic commands are: 

`module overview` - shows a brief list of all available modules, and the number of distinct versions<br> 
`module avail` - shows all available main modules<br> 
`module -t avail` - shows a _terse_ single column list of the available modules<br> 
`module avail [SOFTWARE-NAME or KEYWORD]` - shows all modules for SOFTWARE-NAME or KEYWORD<br> 
`module spider [SOFTWARE-NAME or KEYWORD]` - shows all possible modules for SOFTWARE-NAME or KEYWORD<br> 
`module load [SOFTWARE-NAME/VERSION]` - loads a specific software version<br> 
`module unload [SOFTWARE-NAME/VERSION]` - unloads a specific software version<br> 
`module list` - lists all currently loaded software modules<br> 
`module purge` - unloads ALL currently loaded software modules<br> 

***IMPORTANT:*** Modules on Wiener are NOT self-contained. You will usually need to load all its dependencies as well. Please use 

`module show software-name/version` 

and then look for the *Required modules* or *Modules required* in the lines starting with *whatis*. 

**Please note:**<br> 

Use the full module name, software/version, to be sure to load the version you need and ensure that your research is consistent and repeatable. In case of a dependencies for modules, the exact version is required as otherwise the software is unlikely to work.

## Interactive jobs 
 
``` 
salloc --nodes=1 --ntasks-per-node=1 --cpus-per-task=1 --mem=50G --job-name=TEST --time=05:00:00 --partition=gpu --gres=gpu:1 srun  --pty /bin/bash -l 
```
 
 
This will log you onto a compute node. To run a job just type as you would usually do on the command line. As `srun` was already used in the above command there is no need to use `srun` to run your executables, it will just mess things up. 

You will need to add a `type` to the --gres part if you are targeting a particular GPU, --gres=gpu:[type]:1. Please see below for the options. 

Once you are done type `exit` on the command line which will stop any processes still running and will release the allocation for the job. 

## Slurm scripts 

### How to submit a job 

You would usually write a slurm script to subimit your jobs. Once you have a script you use `sbatch` to submit this script. For example if you have a script called `first-job-script` then you use<br> 

`sbatch first-job-script`<br> 

to submit the slurm script and your job. 

The different request flags mean the following: 

`#SBATCH --nodes=[number]` - how many nodes the job will use<br> 
`#SBATCH --ntasks-per-node=[number]` - This is 1 for single thread jobs and multi thread jobs. This is 28 (or less if single node) for MPI jobs.<br> 
`#SBATCH --cpus-per-task=[number]` - This is 1 for single thread jobs, number of threads for multi thread jobs. `--cpus-per-task` can be undertstood as `OMP_NUM_THREADS`. <br> 
`#SBATCH --mem=[number M|G|T]` - RAM per job given in megabytes (M), gigabytes (G), or terabytes (T). <br> 
`#SBATCH --mem-per-cpu=[number M|G|T]` - alternative to the request above, only relevant to MPI jobs.<br> 
`#SBATCH --gres=gpu:[type]:[number-of-gpus]` - to request the use of 1 or more GPUs. `[type]` can be `tesla` with up to 2 GPUs per node or `tesla-smx2` with up to 4 GPUs per node. <br> 
`#SBATCH --time=[hours:minutes:seconds]` - time the job needs to complete. <br> 
`#SBATCH -o filename` - filename where the standard output should go to<br> 
`#SBATCH -e filename` - filename where the standard error should go to<br> 
`#SBATCH -job-name=[Name]` - Name for the job that is seen in the queue<br> 
`#SBATCH --partition=gpu`<br> 
`#SBATCH --array=[range]` - Indicates that this is and array job with range number of tasks.<br> 
`srun` - runs the executable and will receive info on number of threads, memory, etc from Slurm. There is no need to specify them here. 

See `man sbatch` and `man srun` for more options (use arrow keys to scroll up and down and `q` to quit) 


### Example scripts  

The following provide example scripts that can be adapted to needs and different software used. 

```
#!/bin/bash 
#SBATCH --job-name=my-gpu-job 
#SBATCH --nodes=1 
#SBATCH --gres=gpu:tesla:1 
#SBATCH --ntasks-per-node=1 
#SBATCH --cpus-per-task=7 
#SBATCH --mem-per-cpu=5G 
#SBATCH --partition=gpu 
#SBATCH --time=00:10:00

```


The `--gres` (global resource) parameter is used to specify how many GPUs are required per node. This option is essential as otherwise Slurm will not allocate a GPU to the job. Wiener has nodes that can provide two or four GPUs. It takes the form: 
gpu:[type]:[number-of-gpus]. 

Wiener has two types of GPU available: 

|Name|GPU Memory|Gres Type| 
|----|-----|-----|
|Tesla V100-PCIE|16GB|tesla| 
|Tesla V100-SXM2|32GB|tesla-smx2| 


**Note: the gres type is `smx2` and it does not match the actual GPU name SXM2** 

Wiener has 17 nodes that have two V100-PCIE GPUs and 15 nodes that have four V100-SXM2 GPUs.<br> 
If you simply want to schedule a job and do not care what type of GPU is allocated to your job, your gres string would be `--gres=gpu:1`. This would run your job on the first available node.<br> 
If you require a GPU that has 32GB of memory you would specify `--gres=gpu:tesla-smx2:1`.<br>
If you want to run your job on multiple GPUs only the SXM2 nodes can provide three or four GPUs on the same node e.g., `--gres=gpu:tesla-smx2:4`. 

### Job commands in scripts 

The following command run the python code once the job is allocated. In this example we will use the anaconda environment manager. 

Load the CUDA module which provides the GPU libraries required by python<br>
`module load cuda/11.7.0` 

Load the anaconda module<br>
`module load anaconda/3.7` 

Initialise anaconda (this is broken for anaconda/3.5)<br>
`eval "$(conda shell.bash hook)"`

Activate your environment.<br>
`conda activate myenv`

Run your code<br>
`srun python my-python-code.py`


For detailed instructions on how to work with anaconda and conda environments please see the [conda guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/conda-environment.md)

A complete slrum script example looks like this (this will need to be adapted to currects paths and programs before using it.)

```
#!/bin/bash 
#SBATCH --job-name=my-gpu-job 
#SBATCH --nodes=1 
#SBATCH --gres=gpu:tesla:1 
#SBATCH --ntasks-per-node=1 
#SBATCH --cpus-per-task=7 
#SBATCH --mem-per-cpu=5G 
#SBATCH --partition=gpu 
#SBATCH --time=00:10:00

module load cuda/11.7.0
module load anaconda/3.7

eval "$(conda shell.bash hook)"
conda activate myenv
srun python my-python-code.py

```

 

### How to check jobs in SLURM 

 
 

#### Just your jobs 

`squeue -u YourUsername` -- will only print your jobs<br> 

`squeue -u $USER`<br> 

`squeue --me`<br> 

 
 

#### Some formatting ideas for more detailed reports 

 
 

Here are some other useful additions to the squeue command. For information on what all these means please consult the man pages. 
 

``` 
squeue -o "%12i %7q %.9P %.20j %.10u %.2t %.11M %.4D %.4C %.14b %8m %16R %18p %10B %.10L"  

JOBID QOS PARTITION NAME USER STATE TIME NODE CPUS TRES_PER_NODE MIN_MEMORY NODELIST(REASON) PRIORITY EXEC_HOST TIME_LEFT 
``` 

sinfo is used to obtain information about the actual nodes. Here some useful examples. 

```
sinfo

PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
```

```
sinfo -O Partition,NodeList,Nodes,Gres,CPUs

PARTITION  NODELIST  NODES  GRES  CPUS
```
 
```
sinfo -o "%.P %.5a %.10l %.6D %.6t %N %.C %.E %.g %.G %.m"

PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST CPUS(A/I/O/T) REASON GROUPS GRES MEMORY
```


 

 
