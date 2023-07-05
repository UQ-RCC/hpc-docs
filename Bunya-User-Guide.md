# Bunya user guide

## Quick links

* [Connecting to Bunya](https://github.com/UQ-RCC/hpc-docs/blob/main/Bunya-User-Guide.md#connecting)
* [Transferring files](https://github.com/UQ-RCC/hpc-docs/blob/main/Bunya-User-Guide.md#file-transfer)
* [Software on Bunya](https://github.com/UQ-RCC/hpc-docs/blob/main/Bunya-User-Guide.md#software)
* [Using software containers on Bunya](https://github.com/UQ-RCC/hpc-docs/blob/main/Bunya-User-Guide.md#using-software-containers-on-bunya)
* [Interactive batch jobs](https://github.com/UQ-RCC/hpc-docs/blob/main/Bunya-User-Guide.md#interactive-jobs)
* [SLURM scripts and examples](https://github.com/UQ-RCC/hpc-docs/blob/main/Bunya-User-Guide.md#slurm-scripts)
* [How to check jobs in SLURM](https://github.com/UQ-RCC/hpc-docs/blob/main/Bunya-User-Guide.md#how-to-check-jobs-in-slurm)
* [RCC's interactive job script builder for SLURM](https://shiny.rcc.uq.edu.au/SLURM/)

## General HPC information 

General HPC training is available via the [RCC and QCIF Training resources](https://www.qcif.edu.au/training/hpc-training-resources/).

To get a basic understanding of what you need to be aware of when using HPC for your research please listen to the following videos:

[Connecting to HPC via putty](https://youtu.be/oP_5JJrMm1U)<br>
[Transferring files with FileZilla](https://youtu.be/9ABMxcKqfkQ)<br>
[Where does my data go on HPC](https://youtu.be/cNW7F9V1plA)<br>
[Directories (folders) I should be aware of on HPC](https://youtu.be/rgfbORJLOa8)<br>
[Message of the day (info on current status and problems)](https://youtu.be/B33OKA2QwyI)<br>
[Relative and absolute path (common problem in user scripts)](https://youtu.be/XBG7QpGGY9E)<br>
[How to load installed software](https://youtu.be/AN0zqXj06N4)<br>
[Why no calculation should be run on the login nodes](https://youtu.be/FYqzSP6HWs8)<br>


For UQ users and QCIF users with a QRIScloud collection please also listen to

[General overview of Q RDM](https://youtu.be/zI3jQfaSyCQ)<br>
[Q RDM on HPC](https://youtu.be/kX1k--eXndM)<br>

## Hardware (CPUs, space, RDM)

- Bunya currently has around 6000 cores, with 96 physical cores per compute node.
  - (2 \* 48 core CPUs per node).
- The queue allows 2 \* 96 = 192 threads per compute node (requested by `--cpus-per-task`)  
- These CPUs are based on AMD (epyc3 Milan). They are not Intel CPUs and any software that has been compiled on other HPCs with Intel CPUs will be required to be recompiled on Bunya.
- These CPU cores are based on the industry standard x86\_64 architecture.
- Each standard Bunya compute node has 2TB of RAM (2000000M is the maximum that can be requested in jobs).
- There are also 3 high memory nodes that each have 4TB of RAM (4000000M is the maximum that can be requested in jobs).
- Bunya is currently CPU only for the standard user. The standard queues do not have GPU hardware resources associated with them yet.

- Users have a location in `/home` and `/scratch/user`.
- The quota in `/home` is 50GB and 1 million files
- The quota in `/scratch/user` is 150GB and 100000 files.
- User can use the command `rquota` to check on quotas and usage.
- Users can request a shared scratch space for their group if more space is required. Email rcc-support@uq.edu.au for the application form.

- RDMs are located in `/QRISdata`. These are automounted and there is no need to request a RDM to be mounted on Bunya. 
- Use `ls /QRISdata/QNNNN/` (the `/` at the end is important) or `cd /QRISdata/QNNNN` to *see* your RDM (where QNNNN is your RDM number). Due to the automount the RDM needs to be *used* to be *seen*.


# Guide

## Connecting

Set 1 of the [Training resources](https://www.qcif.edu.au/training/hpc-training-resources/) explains how to use Putty to connect to a HPC with the basics found [here](https://youtu.be/oP_5JJrMm1U). To connect to Bunya please use:

Hostname: bunya.rcc.uq.edu.au<br>
Port: 22

For those using command line ssh:<br>
`ssh username@bunya.rcc.uq.edu.au`

***Bunya enforces MFA (multi factor authentication).***

For UQ users, this will use their DUO MFA that is used for all other access to UQ resources.

QCIF users are required to go here [https://services.qriscloud.org.au/credential](https://services.qriscloud.org.au/credential) and set up an **Authenticator App**.

Users will first be asked for their password (or key). After users have entered this, they will see one or more options given. Choose the option you wish to use and type the respective number on the command line. If you have only set up one MFA option for your account, it will use this option automatically.

For UQ users, you will authenticate via DUO, as you do for other logins at UQ.

For QCIF users, you will be asked to enter the one-time-authentication code.

After this you will be logged into Bunya.

**Note for QCIF users:**
QCIF users (non UQ) are required to set up an ssh-key to gain access to Bunya. For this users are required to provide a public ssh key as part of the application procedure.

## File Transfer

We recommend to use command line `scp` and `sftp`. The are accessible to all users, via a shell for Linux and Mac users and via WSL and `cmd` for Windows users.

`scp file username@bunya.rcc.uq.edu.au:/path-to-place-for-file/`

For example

`scp test.dat username:bunya.rcc.uq.edu.au:/scratch/user/username/`

will copy the file `test.dat` to the user's scratch directory.

`sftp username@bunya.rcc.uq.edu.au`

You will see `sftp>` as prompt once you have logged in.

`ls` and `cd` work as usual on the Bunya end. Use `lls` to list files on your desktop/laptop and `lcd` to change directories on your desktop/laptop.

Use `get` to pull files and directories from Bunya to your desktop/laptop and 
use `put` to move files and directories from your desktop/laptop to Bunya.

Windows users can also use WinSCP if they require a graphical SFTP client. WinSCP allows the MFA authentication without extra setup. WinSCP also allows mutiple file and directory transfer without having to re-enter the MFA passcode.

FileZilla is no longer recommeneded, but if required please find the details here:

The basic use of FileZilla for file and data transfer is shown [here](https://youtu.be/9ABMxcKqfkQ).

If you experience problems with disconnection, then try this: Go to Edit -\> Settings and change the number under "Timeout" from 20 seconds to 120 or more.

With MFA you need to use an interactive session in FileZilla to connect. Click on the icon directly under "File" (left top corner). Please do not enter anything in the boxes for hostname etc or click the Qickconnect button. 

[FileZilla picture 1](FileZilla-n.png) 

Then click on *New site* and use "bunya.rcc.uq.edu" as the *Host*, "22" for *Port* and select "SFTP" for the *Protocol*. Be sure to select "Interactive" as the *Logon Type*. Enter your "username for Bunya" under *User*. Then click *Connect*.

[FileZilla picture 2](FileZilla-2-n.png)

You then might need to accept the host key by clicking *OK*.

[FileZilla picture 3](FileZilla-3-n.png)

You will then be asked for your password for your username. Please enter this.

Then you will see the reqeust for the multifactor authentication. Please enter the 6 number passcode from your authenticator app (DUO or other) here. It is advisable to click "refresh" on the passcode first or check the timer on the passcode before entering the passcode.

[FileZilla picture 4](FileZilla-4-n.png)



## Software

The [training resources](https://www.qcif.edu.au/training/hpc-training-resources/) have a short video on how to use [software modules](https://youtu.be/AN0zqXj06N4) to load installed software on HPC.

The basic commands are:

`module overview` - shows a brief list of all available modules, and the number of distinct versions<br>
`module avail` - shows all available main modules<br>
`module --show_hidden avail` - shows all available modules, including those that are normally hidden<br>
`module -t avail` - shows a _terse_ single column list of the available modules<br>
`module avail [SOFTWARE-NAME or KEYWORD]` - shows all modules for SOFTWARE-NAME or KEYWORD<br>
`module spider [SOFTWARE-NAME or KEYWORD]` - shows all possible modules for SOFTWARE-NAME or KEYWORD<br>
`module load [SOFTWARE-NAME/VERSION]` - loads a specific software version<br>
`module unload [SOFTWARE-NAME/VERSION]` - unloads a specific software version<br>
`module list` - lists all currently loaded software modules<br>
`module purge` - unloads ALL currently loaded software modules<br>

Bunya uses EasyBuild to build and install software and modules. Modules on Bunya are self-contained which means users do not need to load any dependencies for the module to work. This is similar to how modules worked on Tinaroo and FlashLite but different to Wiener.

Using `module avail` will show only the main software modules installed. It will not show all the different dependency modules that are also available. To show ALL modules including hidden modules use

`module --show_hidden avail`

Ordinarily, the module command will only search standard pre-configured paths, but you can modify the search path within your current session. 
If you have created some personal module files and would like to use them, then you need to add the directory containing those personal software modules to the search path using the following command

`module use path_to_where_you_keep_your_modules`

The `-a` option can be used to _append_ the search path instead of pre-pending it. 
The command `module unuse path_to_where_you_keep_your_modules` will reverse this temporary change (or you could login again). 
You can make sure it is always set by modifying your `$HOME/.bashrc` file.  

**Please note:**
- Use the full module name, software/version, to be sure to load the version you need and ensure that your research is consistend and repeatable
- Modules denoted as the default (D) are only the default in their module list, `/sw/auto/rocky8.6/epyc3/modules/all` or `/sw/local/rocky8.6/noarch/qcif/modules` for example. If a software is available as a module in more than one list then users are required to use the full module name (software/version).
- Most system libraries and tools (gfortran, gcc, eigen, etc) are required to be loaded as modules. Users should check `module --show_hidden avail` if they get a *library not found error* to see if it is avialable via a module.


### How to build your own software

#### Building additional packages for R

The installation of R on Bunya comes with many packages provided (see `module help r`) that can be loaded using the library() function.
Additional R packages (ones that you need but don't have provided already need to be built using the `install.package()` function _within_ R. 
**Note: R packages that were built for Tinaroo, or for a different version of R will NOT work properly or at all on Bunya.**
We recommend that you delete all packages built with/for/on Tinaroo and FlashLite and run `install.packages()` again.

#### Building Python environments ####

Similary to information about for R packages. Python environments built with/for/on Tinaroo and FlashLite need to be reinstalled on Bunya.

Please see [here](conda-environment.md) for more information on how to build conda environments on Bunya.

#### Building software using EasyBuild

Users can use EasyBuild to build their own software against existing modules on Bunya.

[https://docs.easybuild.io/en/latest/index.html](https://docs.easybuild.io/en/latest/index.html)

EasyBuild recipes can be found for a very wide range of software. Some might need tweaking for newer versions, but it often is relatively easy. You can also write your own.

Users can build into their own home directory but use all exisiting software and software tool chains that are already available. Users need to load the EasyBuild module first:

`module load easybuild`

For example, if you create a folder called EasyBuild in your home directory and have a recipe located in this directory you can build the software via this command.

```
eb --prefix=/home/YourUsername/EasyBuild --installpath=/home/YourUsername/EasyBuild --buildpath=/home/YourUsername/EasyBuild/build --robot=/home/YourUsername/EasyBuild ./EasyBuild-recipe-file.eb
```

If you add the `-D` option, it will do a dry run first. Please use `eb -H` to get the help manual.

There are currently over 16,000 sample easybuild (.eb) recipe scripts available after you load the easybuild module.
The `eb -S  searchtext` will return all .eb scripts with a case insensitive match. You may need to refine your search. 

The names of sample easy build scripts include one of the following labels that represent the toolchain to be used when building the software.
As you can see, the toolchains are built upon a specific version of compiler. The vast majority of the software for Bunya has been built with one of the Solid GCC based toolchains.

|Label|Compiler|Status|
|:---|:---:|:---:|
|foss-2022a|GCC 11.3.0|Solid|
|GCCcore-11.3.0|GCC 11.3.0|Solid|
|foss-2021a|GCC 10.3.0|Solid|
|GCCcore-10.3.0|GCC 10.3.0|Solid|
||||
|intel-2021a|Intel 2021.2.0|Solid|
||||
|foss-2020a|GCC 9.3.0|Not exhaustively tested|
|GCCcore-9.3.0|GCC 9.3.0|Not exhaustively tested|
|foss-2019a|GCC 8.2.0-2.31.1|Not exhaustively tested|
|GCCcore-8.2.0|GCC 8.2.0-2.31.1|Not exhaustively tested|

Many older versions and toolchains may be present amongst the sample eb scripts (recipes). 

The specific version of the software you need to build _may_ have an eb script available for one of our "Solid" toolchains available on Bunya. That makes building software quicker and more straightforward because the build can rely on pre-existing components. 

If a "Solid" version doesn't exist then you have two choices and both may involve extra work. 
You could proceed with attempting to build it using the .eb file without modification. This will build everything that it needs (i.e. _all_ dependencies) for that software so can take many hours to complete. It may entail minor fixes along the way to get it all successfully built.  
Alternatively, you could adapt the eb script to make it compatible with one of the Solid toolchains listed above. This involves tracing dependencies (exact versions matter).

Users who have a working EasyBuild recipe and have tested that the software installed as such is working on Bunya can offer their EasyBuild recipe to be uploaded to the suite of cluster wide installed software and it would then be available via modules. It is preferable that the recipe be for one of the "Solid" toolchains, unless there is a strong reason because of compatibility with other software.


### Using software containers on Bunya

The software build management system on Bunya is better equipped to support a range of software on the "bare-metal". There is, still, support on Bunya for software container technology to provide greater flexibility for Bunya users.

#### Background

Software containers is a generic technology. It permits pre-built image files containing non-standard operating systems and software to be run like they are installed on the HPC. Docker, Shifter, Singularity/Apptainer are like different "brands" of subsystems to support software containers.

Bunya uses [*Apptainer*](https://apptainer.org). Singularity was rebranded as Apptainer when it joined the Linux Foundation. Currently, the version of Apptainer currently installed on Bunya (v1.1.3) is newer than the Singularity (v3.8.0).

Apptainer is *not* installed on the Bunya login nodes. Apptainer is installed into the operating system on every compute node. You must use an interactive job via the batch system to be able to reach compute nodes and and use a software container. You do *not* need to load a software module to use the apptainer command.

#### Where and how to build a software container

Singularity/Apptainer software containers need to be built on systems where the user has system admin access. 
So, regular users won't be able to _build_ software containers on Bunya. 
However, you will be able to download/upload software containers and run them on Bunya.
You can utilise software containers from public repositories, or build your own on a suitable external system and bring it onto Bunya.

#### How to run a software container on Bunya

For now, you will need to ...

* the apptainer/singularity command is automatically in your PATH (they are now installed into `/usr/bin/` on all Bunya _compute_ nodes but _not_ login nodes)
* set environment variables that govern the location of where the container will store temporary files.<br> 
Specifically, you may run into /home quota trouble if you do not set the **SINGULARITY_CACHEDIR** and **SINGULARITY_TMPDIR** where you have sufficient space (such as `/scratch/user` or `/scratch/project`)
* provide a complete apptainer/singularity command line invocation including bind mounts.

## Interactive jobs

### Do not run on the login nodes

Users are reminded that no calculation, no matter how quick or small, should be run on the login nodes. So no, the quick python or R or bash script or similar should NOT be just quickly run from the command line as it is so much more convenient. **All calculations are required to be done on the compute nodes.**

Users can use interactive jobs which will give them that command line feel and flexibility and allow the use of graphical user interfaces.

Users have access to a `debug` queue for quick testing of new jobs and codes etc.

### Interactive jobs

User should use interactive jobs to do quick testing and if they need to use a graphical user interface (GUI) to run their calculations. This could include jupyter, spider, etc. salloc is used to submit an interactive job and you should specify the required resources via the command line. IMPORTANT: Interactive jobs should be limited to a single node. Multinode jobs are required to be submitted as a batch job.

**Use this full command line to create an interactive session on a compute node. You must combine `salloc` and `srun` to ensure that your processing happens on a Bunya compute node and not on the login node.**

```
salloc --nodes=1 --ntasks-per-node=1 --cpus-per-task=1 --mem=50G --job-name=TEST --time=05:00:00 --partition=general --account=AccountString srun --export=PATH,TERM,HOME,LANG --pty /bin/bash -l
```
You can use the command<br>
`hostname`<br>
to see if you are on a compute node or not. If this shows `bunya1`, `bunya2`, or `bunya3` you are still on a login node. Do not start your calculation, compile or environment install on a login node. Make sure you are on a compute node.

Please use `--partition=general` or `--partition=debug` unless you have been given permission to use `ai`, `gpu` or `aibn_omara`. The `debug` parition has a walltime limit of 1 hour. Use the `groups` command to list your groups- Bunya Account Strings will begin a_ .

If you need to run a GUI then add the option `--x11` to the `salloc` part.

For an interactive session on the `gpu`, `ai` or `aibn_omara` partitions you will need to add `--gres=gpu:[number]` to the `salloc` request. (Note: The A100 GPU has been removed from the `gpu` partition until further notice.) See below for more information.

This will log you onto a node. To run a job just type as you would usually do on the command line. As `srun` was already used in the above command there is no need to use `srun` to run your executables, it will just mess things up.

Once you are done type `exit` on the command line which will stop any processes still running and will release the allocation for the job.

Alternatively, if you use _just_ an `salloc` on the login node, then you _must_ use `srun` to run your command otherwise it will start running on login node and that is not fair on other users.



### Interactive MPI jobs only

Instructions for interactive MPI jobs can be found [here](MPI-interactive.md)

## Available partitions

The available partitions on Bunya are
```
general
debug
gpu
ai
aibn_omara
```

The `ai` and `aibn_omara` partitions are restricted to specific groups and are not open to other users.

`general`<br>
Maximum walltime: 2 weeks (14 days, 336 hours)<br>
CPU only partition<br>
This should be used for the majority of jobs on Bunya.<br>

`debug`<br>
Maximum walltime: 1 hour<br>
Maximum jobs per user: 2<br>
CPU only partition<br>
**Default** partition which means jobs will be queued there if no partition is specified. <br>
This has higher priority than `general` and should be used for testing and quick interactive session. It should **NOT** be used for production calculations. <br>

`gpu`<br>
Maximum walltime: 1 week (7 days, 168 hours)<br>
Maximum GPUs per user: 3<br>
GPU partition<br>
2 AMD Mi210 per node (2 nodes)<br>

`ai`<br>
Restricted access<br>
Maximum walltime: 1 week (7 days, 168 hours)<br>
Maximum GPUs per user: 3<br>
GPU partition<br>
3 NVIDIA A100 per node (3 nodes)<br>

`aibn_omara`<br>
Restricted access<br>
Maximum walltime: 1 week (7 days, 168 hours)<br>
GPU partition<br>
2 A100 per node (1 node)<br>


## Slurm scripts

Users should keep in mind that Bunya has 96 cores (192 threads) per node. 96 cores (`--ntask-per-node=96`)  192 threads (`--cpu-per-task=192`)  is therefore the maximum a multi thread job can request. Please note not all calculations scale well with cores, so before requesting all 96/192 cores/threads **do some testing first**.

The Pawsey Centre has an excellent guide on how to [migrate from PBS to SLURM](https://support.pawsey.org.au/documentation/display/US/How+to+Migrate+from+PBS+Pro+to+Slurm). The Pawsey Centre also provides a good general overview of [job scheduling with Slurm](https://support.pawsey.org.au/documentation/display/US/Job+Scheduling) and [examples workflows](https://support.pawsey.org.au/documentation/display/US/Example+Workflows) like array jobs.

### How to submit a job

You would usually write a slurm script to subimit your jobs. Once you have a script you use `sbatch` to submit this script. For example if you have a script called `first-job-script` then you use<br>

`sbatch first-job-script`<br>

to submit the slurm script and your job.

Below are examples for single thread, single node but multiple threads, MPI, and array job submission scripts. 
The different request flags mean the following:

`#SBATCH --nodes=[number]` - how many nodes the job will use<br>
`#SBATCH --ntasks-per-node=[number]` - This is 1 for single thread jobs and multi thread jobs. This is 96 (or less if single node) for MPI jobs.<br>
`#SBATCH --ntasks=[number]` - total number of tasks of the job. Relevant to MPI jobs (it is usually 1 for non-MPI jobs) and should be set to the total number of threads for the job (what you woudl use with the -np or -n option for mpirun). This should be used instead of requesting number of nodes and tasks per node to enable faster scheduleing of MPI jobs.<br> 
`#SBATCH --cpus-per-task=[number]` - This is 1 for single thread jobs, number of threads for multi thread jobs. `--cpus-per-task` can be undertstood as `OMP_NUM_THREADS`. This is 1 for MPI jobs.<br>
`#SBATCH --mem=[number M|G|T]` - RAM per job given in megabytes (M), gigabytes (G), or terabytes (T). The full memory of 2TB or 4TB is not available to jobs, therefore jobs asking for 2TB or 4TB (2000G or 4000G) will NOT run. Ask for `2000000M` to get the maximum memory on a standard node. Ask for `4000000M` to get the maximum memory on a high memory node. See note below why.<br>
`#SBATCH --mem-per-cpu=[number M|G|T]` - alternative to the request above, only relevant to MPI jobs.<br>
`#SBATCH --gres=gpu:[type]:[number]` - to request the use of GPU on a GPU node. On the `gpu` partition and `aibn_omara` partition there are 2 per node and on the `ai` partition there are 3 per node. Please see the example scripts below for the available types of GPUs<br>
`#SBATCH --time=[hours:minutes:seconds]` - time the job needs to complete. Partition limits: `general` = 336 hours (2 weeks), `debug` = 1 hour, `ai,gpu,aibn_omara` = 168 hours (1 week).<br>
`#SBATCH -o filename` - filename where the standard output should go to<br>
`#SBATCH -e filename` - filename where the standard error should go to<br>
`#SBATCH -job-name=[Name]` - Name for the job that is seen in the queue<br>
`#SBATCH --account=[Name]` - AccountString for your research or accounting group, all AccountStrings start with `a_`, use the `groups` command to list your groups<br>
`#SBATCH --partition=general/gpu/debug/ai/aibn_omara`<br>
`#SBATCH --array=[range]` - Indicates that this is and array job with range number of tasks.<br>
`srun` - runs the executable and will receive info on number of threads, memory, etc from Slurm. There is no need to specify them here.

See `man sbatch` and `man srun` for more options (use arrow keys to scroll up and down and `q` to quit)

***Default partition is debug*** If you do not specify a partition when you submit you get the default partition.The default partition is `debug` which will give you are bare minimum of resources. For example the maximum walltime in the `debug queue` is 1 hour. Most users would want to run in the `general` partition. Important, the slurm defaults are usually not sufficient for most user jobs. If you want appropriate resources, you are required to request them.

***Standard outout and error***: Using the `SBATCH` options `-o` and `-e` with a `filename` in a script will result in the standard error and standard output file to appear as soon as the job starts to run. This behaviour is different to standard PBS behaviour on Tinaroo and FlashLite (unless you specified paths for those files there too) where the standard error, .e, and standard output, .o, files only appeared when the job was finished or had crashed.

***Default working directory***: In Slurm your job will start in the directory/folder you submitted from. This is different to PBS behaviour on Tinaroo/FlashLite where your job started in your home directory. So on Bunya, using slurm, there is no need to change into the job directory, unless this is different to the directory you submitted from.

***$TMPDIR***: If your job produces temporary files during the calculation or if you need a space to write to that does not impact your quotas in `/home`, `/scratch/user` or `/scratch/project` then please use **$TMPDIR** during your calculations. **$TMPDIR** is automatically created at the start of a job and is then automatically deleted at the end of the job. It is therefore the best place to write temporary files (those not needed after the calculation is done) to. If you use **$TMPDIR** for output you wish to keep then please make sure you copy all needed files to a location in `/home`, `/scratch/user`, `/scratch/project` or `/QRISdata`. A big (all in one go) copy from **$TMPDIR** to `/QRISdata` (RDM) at the end of a job is possible.

***Note on maximum memory requests:*** The standard compute node has 2TB of physical memory available (or 4TB for the 3 high memory compute nodes). Not all of this can be given to jobs running on the compute node as the Linux operating system also needs resources. This is why the maximum requestable memory has been capped at 2000000MB for the standard compute nodes and 4000000MB for high memory compute nodes. 

So why is 2000000MB not the same as 2TB? 1024 MB = 1 GB and 1024 GB = 1 TB. This means 2000 GB = 2048000 MB which is larger than 2000000M which is set as the maximum available memory on a standard compute node.

***Accounting has now been switched on and will be enforced. Users cannot run jobs without a valid AccountString. Type `groups` on the command line to check if you have one. All valid AccountStrings start with `a_` and are all lower case letters. If you do not have a valid AccountString then please contact your supervisor. AccountStrings and access are managed by research groups and group leaders. Groups who wish to use Bunya are required to apply to set up a group with a valid AccountString. Only group leaders can apply to set up such a group. A PhD student or postdoc without their own funding and group should not apply. Applications can be made by contacting [rcc-support@uq.edu.au](mailto:rcc-support@uq.edu.au).***


### Simple script for AI GPUs.

**Nodes bun003, bun004, and bun005. AI GPUs are restricted to a specific set of users. If you have not been given explicit permission you cannot use these. Only certain AccountStrings have access to these GPUs. If you should and cannot run a job please contact your supervisor.**


`#!/bin/bash --login`<br>
`#SBATCH --nodes=1`<br>
`#SBATCH --ntasks-per-node=1`<br>
`#SBATCH --cpus-per-task=1`<br>
`#SBATCH --mem=10G`<br>
`#SBATCH --job-name=Test`<br>
`#SBATCH --time=1:00:00`<br>
`#SBATCH --partition=ai`<br>
`#SBATCH --account=AccountString`<br>
`#SBATCH --gres=gpu:1 #you can ask for up to 3 here`<br>
`#SBATCH -o slurm.output`<br>
`#SBATCH -e slurm.error`<br>
<br>
`module-loads-go-here`<br>
<br>
`srun executable < input > output`<br>



### Simple script for AMD GPUs.

**Nodes bun001 and bun002. These are AMD GPUs. You most likely will need to compile your own code or use a container to run on these. See the [AMD Infinity Hub](https://www.amd.com/en/technologies/infinity-hub) for some available containers**

`#!/bin/bash --login`<br>
`#SBATCH --nodes=1`<br>
`#SBATCH --ntasks-per-node=1`<br>
`#SBATCH --cpus-per-task=1`<br>
`#SBATCH --mem=10G`<br>
`#SBATCH --job-name=Test`<br>
`#SBATCH --time=1:00:00`<br>
`#SBATCH --partition=gpu`<br>
`#SBATCH --account=AccountString`<br>
`#SBATCH --gres=gpu:mi210:1 #you can ask for up to 2 here`<br>
`#SBATCH -o slurm.output`<br>
`#SBATCH -e slurm.error`<br>
<br>
`module-loads-go-here`<br>
<br>
`srun executable < input > output`<br>



### Simple script for AIBN_OMARA A100 GPUs.

**Node bun068. The AIBN_OMARA A100 GPUs are restricted to a specific set of users. If you have not been given explicit permission you cannot use these. Only certain AccountStrings have access to these GPUs. If you should and cannot run a job please contact your supervisor..**

`#!/bin/bash --login`<br>
`#SBATCH --nodes=1`<br>
`#SBATCH --ntasks-per-node=1`<br>
`#SBATCH --cpus-per-task=1`<br>
`#SBATCH --mem=10G`<br>
`#SBATCH --job-name=Test`<br>
`#SBATCH --time=1:00:00`<br>
`#SBATCH --partition=aibn_omara`<br>
`#SBATCH --account=AccountString`<br>
`#SBATCH --gres=gpu:a100:1 #you can ask for up to 2 here`<br>
`#SBATCH -o slurm.output`<br>
`#SBATCH -e slurm.error`<br>
<br>
`module-loads-go-here`<br>
<br>
`srun executable < input > output`<br>



### Simple script for CPUs and single node

`#!/bin/bash --login`<br>
`#SBATCH --nodes=1`<br>
`#SBATCH --ntasks-per-node=1`<br>
`#SBATCH --cpus-per-task=1`<br>
`#SBATCH --mem=10G`<br>
`#SBATCH --job-name=Test`<br>
`#SBATCH --time=1:00:00`<br>
`#SBATCH --partition=general`<br>
`#SBATCH --account=AccountString`<br>
`#SBATCH -o slurm.output`<br>
`#SBATCH -e slurm.error`<br>
<br>
`module-loads-go-here`<br>
<br>
`srun executable < input > output`<br>

To ask for more than 1 thread change the line

`#SBATCH --cpus-per-task=12`

To run over 12 threads for example.



### Simple MPI script (using 192 cores, as an example). Using --ntasks will spread the job over multiple nodes where there is space.

`#!/bin/bash --login`<br>
`#SBATCH --ntasks=192`<br>
`#SBATCH --cpus-per-task=1`<br>
`#SBATCH --mem-per-cpu=5G`<br>
`#SBATCH --job-name=MPI-Test`<br>
`#SBATCH --time=1:00:00`<br>
`#SBATCH --partition=general`<br>
`#SBATCH --account=AccountString`<br>
`#SBATCH -o slurm.output`<br>
`#SBATCH -e slurm.error`<br>
<br>
`module-loads-go-here`<br>
<br>
`srun executable < input > output`<br>



### Job Arrays

Here is one example of an array job script with 5 array tasks.

`#!/bin/bash --login`<br>
`#SBATCH --job-name=testarray`<br>
`#SBATCH --nodes=1`<br>
`#SBATCH --ntasks=1`<br>
`#SBATCH --cpus-per-task=1`<br>
`#SBATCH --mem=5G`<br>
`#SBATCH --time=00:01:00`<br>
`#SBATCH --account=AccountString`<br>
`#SBATCH --partition=general`<br>
`#SBATCH --output=test_array_%A_%a.out`<br>
`#SBATCH --array=1-5`<br>
<br>
`module-loads-go-here`<br>
<br>
`srun executable < input > output`<br>

Useful variables for array jobs

`$SLURM_ARRAY_JOB_ID` = Job array's master job ID number.<br>
`$SLURM_ARRAY_TASK_COUNT` = Total number of tasks in a job array.<br>
`$SLURM_ARRAY_TASK_ID` = Job array ID (index) number.

### How to check jobs in SLURM

#### Just your jobs
`squeue -u YourUsername` -- will only print your jobs<br>
`squeue -u $USER`<br>
`squeue --me`<br>

#### Some formatting ideas for more detailed reports

Here are some other useful additions to the squeue command. For information on what all these means please consult the man pages.

```
squeue -o "%.18i %.9P %.8j %.8u %.8T %.10M %.9l %.6D %.10a %.4c %R"
JOBID  PARTITION  NAME  USER  STATE  TIME TIME_LIMIT NODES  ACCOUNT  MIN_CPU  NODELIST(or REASON)
```

```
squeue -o "%12i %7q %.9P %.20j %.10u %.2t %.11M %.4D %.4C %.14b %8m %16R %18p %10B %.10L" 
JOBID QOS PARTITION NAME USER STATE TIME NODE CPUS TRES_PER_NODE MIN_MEMORY NODELIST(REASON) PRIORITY EXEC_HOST TIME_LEFT
```
`squeue -o "%.7i %.9P %.8j %.8u %.2t %.10M %.6D %C"`

sinfo is used to obtain information about the actual nodes. Here some useful examples.

```
sinfo -o "%n %e %m %a %c %C"
which yields
HOSTNAMES FREE_MEM MEMORY AVAIL CPUS CPUS(A/I/O/T)
```

`sinfo -O Partition,NodeList,Nodes,Gres,CPUs`<br>
`sinfo -o "%.P %.5a %.10l %.6D %.6t %N %.C %.E %.g %.G %.m"`

#### How to know what resources are actually being utilised by a job?

It is also very important that your jobs do not occupy valuable HPC resources and _not_ utilise them.
The fairshare system calculates your usage based on the resources you requested.
If you order a lot of food, but you don't eat it all, then you still pay for the food you ordered.
HPC's don't have a mechanism like doggy bags ;-)

The fairshare system will account for your usage based on the resources (CPU and/or MEM) you requested even if you did not consume them all. That is because noone else could used those resources while your job was running. A job that finishes earlier than the requested walltime does get charged less.

We often don't know in advance how much resource a set of jobs may require. 
You may have some idea based on calculations you have performed on a workstation or other HPC cluster.
Obviously if your software cannot utilised a GPU resource you would never request it.
But if you have CPU code that is expected to run faster on a single node in shared memory (OpenMP) mode, or on multiple nodes in message passing interface (MPI) mode, then you should be certain that you are getting the performance gains that you expect.

##### A running job

You are able to access any node that is running a job that belongs to you. 

The `squeue --me` command will tell you which node is running your job.
You will need to set up SSH public/private keys and authorized_keys to allow you to easily ssh to any compute node.

Once logged in to the node that is running your job you can use the `top -c -u $USER` command and note the %CPU and RES (memory) values for your processes.

##### A Completed job

The `sacct` command can be used to report CPU and Memory utiisation by a completed job.
```
sacct -p  -a --format JobID,User,Group,State,Cluster,AllocCPUS,REQMEM,TotalCPU,Elapsed,MaxRSS,ExitCode,NNodes,NTasks
yields these metrics
|JobID|User|Group|State|Cluster|AllocCPUS|ReqMem|TotalCPU|Elapsed|MaxRSS|ExitCode|NNodes|NTasks|
```

RCC are working on better ways to report this information, DETAILS TO FOLLOW

