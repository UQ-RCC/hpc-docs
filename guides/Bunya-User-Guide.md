# Bunya user guide

## Quick links

* [General HPC Information](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#general-hpc-information)
* [Bunya Hardware](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#bunya-hardware)
* [Connecting to Bunya](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#connecting)
* [Transferring files](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#file-transfer)
* [Software on Bunya](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#software)
* [Conda on Bunya](conda-environment.md)
* [Using software containers on Bunya](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#using-software-containers-on-bunya)
* [Fair Share on Bunya](FairShare.md)
* [Available hardware and user limits](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#qos-use-and-limits)
* [Interactive batch jobs](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#interactive-jobs)
* [SLURM scripts and examples](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#slurm-scripts)
* [How to check jobs in SLURM](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#how-to-manage-your-jobs-and-cluster-activity-in-slurm)

## General HPC information 

General HPC training is available via the [RCC and QCIF Training resources](https://www.qcif.edu.au/training/hpc-training-resources/).

To get a basic understanding of what you need to be aware of when using HPC for your research please listen to the following videos:

[Connecting to HPC via putty](https://youtu.be/oP_5JJrMm1U)<br>
[Where does my data go on HPC](https://youtu.be/cNW7F9V1plA)<br>
[Directories (folders) I should be aware of on HPC](https://youtu.be/rgfbORJLOa8)<br>
[Message of the day (info on current status and problems)](https://youtu.be/B33OKA2QwyI)<br>
[Relative and absolute path (common problem in user scripts)](https://youtu.be/XBG7QpGGY9E)<br>
[How to load installed software](https://youtu.be/AN0zqXj06N4)<br>
[Why no calculation should be run on the login nodes](https://youtu.be/FYqzSP6HWs8)<br>


For UQ users and QCIF users with a QRIScloud collection please also listen to

[General overview of Q RDM](https://youtu.be/zI3jQfaSyCQ)<br>
[Q RDM on HPC](https://youtu.be/kX1k--eXndM)<br>

## Bunya Hardware

- Bunya has 113 AMD CPU nodes with 96 physical cores per compute node, 2 \* 48 core CPUs per node (roughly 10,600 cores). Cores are requested by `--ntasks-per-node` or `--ntasks` and by `--ntasks-per-core=1`. 
- The queue allows 2 \* 96 = 192 threads per compute node (requested by `--cpus-per-task` and by keeping `--ntasks=1` or `--ntasks-per-node=1`)  
- These CPUs are based on AMD epyc3 Milan (62, phase 1) and epyc4 Genoa (51, 33 phase 2 and 18 in phase 3). They are not Intel CPUs and any software that has been compiled on other HPCs with Intel CPUs will be required to be recompiled on Bunya.
- These CPU cores are based on the industry standard x86\_64 architecture.
- Each Bunya phase 1 standard compute node (epyc3) has 2TB of RAM (2000000M is the maximum that can be requested in jobs).
- Each Bunya phase 2 and 3 standard compute node (epyc4) has 1.5TB of ram (1500000M is the maximum that can be requested in jobs) 
- There are also 3 high memory nodes (epyc3) that each have 4TB of RAM (4000000M is the maximum that can be requested in jobs).

- Bunya has 29 nodes of various types.
- There are 4 H100 SXM5 NVIDIA GPU nodes (intel Xeon SP4) with 4 H100 cards each (16 in total). Each H100 card has 80GB of GPU RAM. 
- There are 7 H100 PCIE NVIDIA GPU nodes (epyc3) with 3 H100 cards each (21 in total). Each H100 card has 80GB of GPU RAM.
- There are 6 L40 NVIDIA GPU nodes (epyc3) with 3 L40 cards each (18 in total). Each L40 card has 48GB of GPU RAM. The L40 are good for visualisation and FP32 workloads.
- There are 2 L40s NVIDIA GPUs nodes (epyc4) with 3 L40s cards each (6 in total). Each L40s card has 48GB of GPU RAM. The L40s are good for visualisation and FP32 and FP16 workloads.
- There is 1 A100 NVIDIA GPU nodes (epyc3) with 3 A100 cards each, 1 A100 NVIDIA GPU node with 2 A100 cards. Each A100 card has 80GB of GPU RAM. 
- There are 2 A100 NVIDIA GPU node with MIG A100 cards leading to 3 MIG slices with 40GB of GPU RAM, 3 MIG slices with 20GB of GPU RAM and 6 MIG slices with 10GB of GPU RAM.
- There are 3 A16 NVIDIA GPU nodes (epyc4) with 12 A16 GPUs each (36 in total). The A16 GPU are good for vizualisation and accelerated desktops.
- There are 3 AMD Mi210 GPU nodes (2 epyc3 and 1 epyc4) with 2 Mi201 cards each (6 in total). Each Mi210 card has 64GB GPU RA.M.
- There are 2 AMD Mi300x GPU nodes (epyc4) with 8 Mi300x cards. Each Mi300x card has 192GB GPU RAM  
- For a full table of all available compute nodes and their features like GPU, Memory and CPUs see [here](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#available-partitions-and-nodes)
 
- Users have a location in `/home` and `/scratch/user`. There are quotas on these locations for total GB _and_ total number of files. Refer to [Bunya UserData Guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-UserData-Guide.md) 
- Users can run the command `rquota` to check on quotas and usage.
- Users can request a shared scratch space for their group if more space is required. Email rcc-support@uq.edu.au for the application form.
- Software and software environments should be installed in `/home` or `/scratch`. Software should not be installed on RDM (`/QRISdata`)
- Jobs should be run from `/scratch`. It is not advisable to use `/home` as the space to run (submit jobs) from. Jobs are not permitted to be submitted from RDM (`/QRISdata`).

- RDMs are located in `/QRISdata`. These are automounted and there is no need to request a RDM to be mounted on Bunya. 
- Use `ls /QRISdata/QNNNN/` (the `/` at the end is important) or `cd /QRISdata/QNNNN` to *see* your RDM (where QNNNN is your RDM number). Due to the automount the RDM needs to be *used* to be *seen*.


# Guide

## Applying for Access

Access to Bunya HPC is not automatic. You need to apply by emailing rcc-support@uq.edu.au or using [this form](https://forms.office.com/r/87rfgvxDnz)

>[!NOTE]
>Applications under staff account preferred. Those applying under a student account will be asked to provide an end date for their access.
>
>You will need to provide current SIX (6) DIGIT FoR code(s).
>If you do not know what a FoR code is or do not have one please contact your supervisor.
>
>It can take up to one week for a new user access to be processed. 

## Introduction to HPC Training

If you would like to attend [Intro to HPC training](https://rcc.uq.edu.au/training-support/training-courses#regular) then the sessions are generally scheduled on the final Tuesday morning of each month (except for December).
You should apply by emailing rcc-support@uq.edu.au. 
You should have your access to Bunya HPC organised prior to attending (noting the point above that it may take up to a week for that to be completed)

## Connecting

>[!CAUTION]
>***Do not share passwords, ssh keys or your multifactor authentication.*** 
>
>This is a violation of UQ's cyber security policy and UQ's conditions of access to RCC infrastructure policy to which every Bunya user agrees to when applying for Bunya access.
>
>Violation of UQ's policies and conditions of access may lead to the suspension of access to RCC infrastructure (temporarily or permanently) and in some cases a report to the Integrity Unit for misconduct.
>
>Here are just some examples that are a violation of UQ's policies (there are others):
>
>* You allow another person to use your account to access Bunya. It makes no difference if they have used Bunya (i.e. ran jobs), or not. And it makes no difference if you logged them in and were there all the time.
>* Another user is struggling to get enough resources (jobs running) for their work. You allow them to use your account to be able to run more jobs. It does not matter if the other user is a fellow student, or you are their supervisor, or you are their friend, or you are their partner etc.
>* You are sharing your computer (work or home) with others and you have set up an ssh key for convenient access. If you are sharing a single local account on the computer, by default there is a single ssh key even if you are accessing different accounts. If you are sharing a computer, you must all have distinct ssh keys stored in separate accounts on the shared computer, or you should not use ssh keys but use passwords only. Best practice would be to set up separate accounts on the shared computer for each person.
>* You have your password or SSH key stored somewhere that another person can access it, and they can gain access to your DUO authenticator. Your account credentials are only to be used by yourself, and not to be shared with anybody including your supervisor or IT support staff.

### How to connect

#### UQ Users

UQ users of Bunya will use their UQ credentials. If you have both staff and student credentials then you will need to use the one that was used to request your access. This is most likely to be your *staff* credential if you have one. Multi-factor authentication is automatically active for UQ users. See below.

#### QCIF (non-UQ) users

QCIF users (non-UQ) will use their QSAC username and password.[https://services.qriscloud.org.au/credential](https://services.qriscloud.org.au/credential)
Multi-factor authentication must also be configured. See below.

#### "onBunya only" users


>[!NOTE]
>
>We get it, but sometimes you need to use the command line to get things done.<br>
>
>Even if you want to use onBunya exclusively, you will need to login using a direct ssh method when you access Bunya for the first time. <br>
>This is required to trigger the proper setup of your account, so that you will be able to use onBunya fully.
>
>A straightforward way to achieve this is to <br>
>1. login into the onBunya Dashboard (https://onbunya.rcc.uq.edu.au) <br>
>2. select Clusters ... Bunya Shell Access  from the drop down menus <br>
>3. enter your password for your Bunya HPC username and your Multi-factor Authentication code when prompted (see MFA section below)<br>
>4. once you are logged in you can use `exit` to logout again.<br>
><br>
>You may find from time to time that you need to query the batch system or perform tasks that require Bunya Shell Access. <br><br>
>Alternatively, you can use an ssh command line client like putty or ssh in a command terminal on a Mac, Linux or Windows PC as described here:


#### Command line SSH Access to Bunya

Set 1 of the [Training resources](https://www.qcif.edu.au/training/hpc-training-resources/) explains how to use Putty to connect to a HPC with the basics found [here](https://youtu.be/oP_5JJrMm1U). To connect to Bunya please use:

Hostname: bunya.rcc.uq.edu.au<br>
Port: 22

For those using command line ssh:<br>
`ssh username@bunya.rcc.uq.edu.au`

#### Bunya enforces MFA (multi-factor authentication)

For UQ users, this will use their DUO MFA that is used for all other access to UQ resources.

QCIF users are required to go here [https://services.qriscloud.org.au/credential](https://services.qriscloud.org.au/credential) and set up an **Authenticator App**.

Users will first be asked for their password (or key). After users have entered this, they will see one or more options given. Choose the option you wish to use and type the respective number on the command line. If you have only set up one MFA option for your account, it will use this option automatically.

For UQ users, you will be asekd to enter the DUO passcode (6 numbers with no spaces).

For QCIF users, you will be asked to enter the one-time-authentication code (6 numbers with no spaces).

After this you will be logged into Bunya.

#### Note for those using MobaXTerm Software

This SSH/X11 client has an experimental feature called "Remote monitoring". 
Please disable it by modifying default behaviour for SSH connections via the main menu _Settings ... SSH ... uncheck Remote-monitoring (Experimental)_ and please don't activate it manually.

#### When Bunya is down for maintenance

Bunya is taken offline 4 times per year (second Tuesday of February, May, August, November) to perform important maintenance work. All users are advised in the weeks leading up to these occasions.

Depending on where the maintenance work has reached when you attempt to login, you may get connection refused or no route to host (because the login nodes are still being worked on) or you may get a login session that closes immediately and automatically with a message:
```
Success. Logging you in...
Bunya is currently down for maintenance

Connection closed by 203.22.86.167 port 22
```

#### What to do when you can't login and it isn't a maintenance day ?

Email rcc-support@uq.edu.au and try to provide as much detail about the situation. 
At the minimum, your Bunya username, where you were trying to connect from (e.g. campus, home, VPN) and the tool you are using to connect with.

## File Transfer

We recommend to use command line `scp` and `sftp`. These are accessible to all users, via a shell for Linux and Mac users and via WSL and `cmd` for Windows users.

### Using scp

From the command line on your PC, type

`scp file username@bunya.rcc.uq.edu.au:/path-to-place-for-file/`

For example

`scp test.dat username@bunya.rcc.uq.edu.au:/scratch/user/username/`

will copy the file `test.dat` to the user's scratch directory.

### Using sftp

From the command line on your PC, type

`sftp username@bunya.rcc.uq.edu.au`

You will see `sftp>` as prompt once you have logged in.

`help` provides a summary of the commands available in sftp.

- Use `pwd`, `ls`, `cd` and `mkdir` to print location, list files, change directory and create a new directory **on the Bunya end**.
- Use `lpwd`, `lls`, `lcd` and `lmkdir` to print your location, list files, change directory and create a new directory **on your desktop/laptop**.
- Use `get` to pull files and directories **from Bunya to your desktop/laptop**.
- Use `put` to push files and directories **from your desktop/laptop to Bunya**.

### Using WinSCP

Windows users can also use WinSCP if they require a graphical SFTP client. WinSCP allows the MFA authentication without extra setup. WinSCP also allows mutiple file and directory transfer without having to re-enter the MFA passcode.

### Using FileZilla ... Don't!

FileZilla is no longer recommended. 

<!---
but if required please find the details here:

The basic use of FileZilla for file and data transfer is shown [here](https://youtu.be/9ABMxcKqfkQ).

If you experience problems with disconnection, then try this: Go to Edit -\> Settings and change the number under "Timeout" from 20 seconds to 120 or more.

With MFA you need to use an interactive session in FileZilla to connect. Click on the icon directly under "File" (left top corner). Please do not enter anything in the boxes for hostname etc or click the Qickconnect button. 

[FileZilla picture 1](../media/FileZilla-n.png) 

Then click on *New site* and use "bunya.rcc.uq.edu" as the *Host*, "22" for *Port* and select "SFTP" for the *Protocol*. Be sure to select "Interactive" as the *Logon Type*. Enter your "username for Bunya" under *User*. Then click *Connect*.

[FileZilla picture 2](../media/FileZilla-2-n.png)

You then might need to accept the host key by clicking *OK*.

[FileZilla picture 3](../media/FileZilla-3-n.png)

You will then be asked for your password for your username. Please enter this.

Then you will see the reqeust for the multifactor authentication. Please enter the 6 number passcode from your authenticator app (DUO or other) here. It is advisable to click "refresh" on the passcode first or check the timer on the passcode before entering the passcode.

[FileZilla picture 4](../media/FileZilla-4-n.png)
-->

## Accessing Compute Nodes from Login Nodes

On Bunya, you are able to login to any compute node that is currently running your job(s). <br>
If you do not have a running job on a compute node you will be unable to connect.

Before you can do that, you will need to set up an SSH keypair on Bunya for use within Bunya.<br> 
**This keypair should only be used within Bunya HPC and NOT for connecting from outside**

On your Bunya login node run command<br>
`ssh-keygen -b 2048 -t rsa`<br>
Press enter for the default filename and location, then press enter (twice) for no password to be set on the private key (see warning above about keeping this key for use within Bunya only).<br>
This should have generated a key pair: `$HOME/.ssh/id_rsa` (the private key) and `$HOME/.ssh/id_rsa.pub` (the public key)

Append the public key contents to your authorized keys file.<br>
`cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys`<br>

Use `squeue --me` to figure out the compute node that is running your job of interest.<br>
Then you can use the `ssh` command to connect to that compute node.

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
- Modules denoted as the default (D) are only the default in their module list, `/sw/auto/rocky8c/epyc3/modules/all` or `/sw/local/rocky8/noarch/qcif/modules` for example. If a software is available as a module in more than one list then users are required to use the full module name (software/version).
- Most system libraries and tools (gfortran, gcc, eigen, etc) are required to be loaded as modules. Users should check `module --show_hidden avail` if they get a *library not found error* to see if it is avialable via a module.

**Please note:**
- The modules in `/sw/auto/rocky8c/epyc3/modules/all` will also be available on the `epyc4` compute nodes and names etc are identical. So there is nothing different do for modules in this list. Modules in `/sw/local/rocky8/epyc3/rcc/modules`, `/sw/local/rocky8/noarch/rcc/modules`, and `/sw/local/rocky8/noarch/qcif/modules` are also available on all `epyc4` compute nodes.
- The GPU nodes will have different modules available and users are advised to log onto a GPU node via an interactive session to see which modules are avialable for the specific GPU architectures. For example, CUDA modules will not be availalbe on CPU nodes, but will be available on the CUDA GPU nodes.<br>
The command that will load the default version of the cuda drivers etc. on a GPU node will be <br>
`module load cuda`<br>
An alternative to using an interactive session on a CUDA node, would be to interrogate the `/sw` filesystem for the versions of cuda that are available.<br>
`ls /sw/auto/rocky8*/*/modules/all/cuda/`

### Compilers

- The GCC compilers are available via the `foss` modules. These contain the complete tool chain, which include the compiler, OpenMPI, FlexiBlas, FFTW and Scalapack.
- Users should use `foss/2021a`, `foss/2022a` or `foss/2023a`
- The Intel compilers are available via the `intel/2021a`, `intel/2022a` or `intel/2023a` modules which include the compiler, IntelMPI and MKL. 

### How to build your own software

***IMPORTANT*** If you are building your own software, especially if you are compiling your own software, you need to be aware of the different architectures, `epyc3` and `epyc4`. Software built on an `epyc3` compute node will run on a `epyc4` compute node **BUT** software built on a `epyc4` compute node will not run on a `epyc3` compute node. If you want ease of use you need to make sure to compile on a `epyc3` compute node. If you want best performance you should compile for a specific architecture but then need to request that architecture for your jobs. 

These AMD guides (in PDF) [EPYC3](https://www.amd.com/content/dam/amd/en/documents/epyc-technical-docs/programmer-references/compiler-options-quick-ref-guide-epyc-7xx3-series-processors.pdf)  [EPYC4](https://www.amd.com/content/dam/amd/en/documents/developer/compiler-options-quick-ref-guide-amd-epyc-9xx4-series-processors.pdf) will be useful to understanding the options you may need to consider for optimising the performance of your code on Bunya. 

***Please note*** **ALL** software builds should be done on a compute node. Processes running on the login nodes, including software builds (conda environments, make-make install, EasyBuild) will most likley be killed if found on the login nodes.


#### Building additional packages for R

The installation of R on Bunya comes with many packages provided (see `module help r`) that can be loaded using the library() function.
Additional R packages (ones that you need but don't have provided already need to be built using the `install.package()` function _within_ R. 
**Note: R packages that were built for Tinaroo, or for a different version of R will NOT work properly, or at all, on Bunya.**
We recommend that you delete all packages built with/for/on Tinaroo and FlashLite and run `install.packages()` again.

Additionally, R packages built on the newer EPYC4 CPU nodes are known _not_ to work on the older EPYC3 CPU nodes. To ensure you build R packages that can be run on both CPU types you must run install.packages() on the older EPYC3. See the section on interactive jobs for how to target the older nodes for building R packages.

#### Building Python and Conda environments ####

Similary to information about for R packages. Python environments built with/for/on Tinaroo and FlashLite need to be reinstalled on Bunya.

Please see [here](conda-environment.md) for more information on how to build conda environments on Bunya.

#### Building software using EasyBuild

Users can use EasyBuild to build their own software against existing modules on Bunya.

[https://docs.easybuild.io/en/latest/index.html](https://docs.easybuild.io/en/latest/index.html)

EasyBuild recipes can be found for a very wide range of software. Some might need tweaking for newer versions, but it often is relatively easy. You can also write your own.

Users can build into their own home directory but use all exisiting software and software tool chains that are already available. Users need to load the EasyBuild module first:

`module load easybuild`

Please note: We usually advise to use the full module, name/version, to load software modules. The easybuild module is an exception as you want to make sure to always have the lastest version to have access to all available recipes.

For example, if you create a folder called EasyBuild in your home directory and have a recipe located in this directory you can build the software via this command. Make sure you are on a compute node before doing this.

```
eb --prefix=/home/YourUsername/EasyBuild --installpath=/home/YourUsername/EasyBuild --buildpath=/home/YourUsername/EasyBuild/build --robot=/home/YourUsername/EasyBuild ./EasyBuild-recipe-file.eb
```

If you add the `-D` option, it will do a dry run first. Please use `eb -H` to get the help manual.

There are currently over 16,000 sample easybuild (.eb) recipe scripts available after you load the easybuild module.
The `eb -S  searchtext` will return all .eb scripts with a case insensitive match. You may need to refine your search. 

The names of sample easy build scripts include one of the following labels that represent the toolchain to be used when building the software.
As you can see, the toolchains are built upon a specific version of compiler. The vast majority of the software for Bunya has been built with one of the Solid GCC based toolchains.

|Toolchain Module|Compiler Base|Status on Bunya|
|:---|:---:|:---:|
|foss/2023a|GCC 12.3.0|Solid|
|gfbf/2023a|GCC 12.3.0|Solid|
|gcc/12.3|GCC 12.3.0|Solid|
|foss/2022a|GCC 11.3.0|Solid|
|gfbf/2022a|GCC 11.3.0|Solid|
|gcc/11.3|GCC 11.3.0|Solid|
|foss/2021a|GCC 10.3.0|Solid|
|gcc/10.3|GCC 10.3.0|Solid|
||||
|intel/2023a|Intel 2023.1.0|Solid|
|intel/2022a|Intel 2022.1.0|Solid|
|intel/2021a|Intel 2021.2.0|Solid|

For more information about the toolchains, refer to the [EasyBuild documentation](https://docs.easybuild.io/common-toolchains/#newest-generations-2022b-and-later)

Many older versions and toolchains may be present amongst the sample eb scripts (recipes). If you choose to build software with a non-Solid toolchain on Bunya, you may find the task quite time consuming as you could end up building the entire toolchain and every dependency from source code. You have been warned ;-)

The specific version of the software you need to build _may_ have an eb script available for one of our "Solid" toolchains available on Bunya. That makes building software quicker and more straightforward because the build can rely on pre-existing components. 

If a "Solid" version doesn't exist then you have two choices and both may involve extra work. 
You could proceed with attempting to build it using the .eb file without modification. This will build everything that it needs (i.e. _all_ dependencies) for that software so can take many hours to complete. It may entail minor fixes along the way to get it all successfully built.  
Alternatively, you could adapt the eb script to make it compatible with one of the Solid toolchains listed above. This involves tracing dependencies (exact versions matter).

Users who have a working EasyBuild recipe and have tested that the software installed as such is working on Bunya can offer their EasyBuild recipe to be uploaded to the suite of cluster wide installed software and it would then be available via modules. It is preferable that the recipe be for one of the "Solid" toolchains, unless there is a strong reason because of compatibility with other software.


### Using software containers on Bunya

The software build management system on Bunya is better equipped to support a range of software on the "bare-metal". There is, still, support on Bunya for software container technology to provide greater flexibility for Bunya users.

#### Background

Software containers is a generic technology term. It provides a mechanism for different operating systems and software that are not available in the host operating system so they can be used safely on the HPC platform. Software containers can be built from a "recipe" or downloaded as pre-built images, often as a stack that is assembled on the fly.

The names Docker, Shifter, Singularity/Apptainer are like different "brands" that support software containers.

Bunya uses [*Apptainer*](https://apptainer.org/docs/user/latest/introduction.html). Apptainer was created when Singularity was rebranded when it joined the Linux Foundation. Currently, the version of Apptainer installed on Bunya is version 1.3.0-1.el8 which is actually newer than the latest Singularity release (v3.8.7).

Apptainer is *not* installed on the Bunya login nodes. Apptainer is installed into the operating system on every compute node. You must use an interactive job via the batch system (or an [onBunya](http://bunya-ondemand.rcc.uq.edu.au/) session) to be able to reach compute nodes and use apptainer. You do *not* need to load a software module to use the apptainer command.

#### How to run a software container on Bunya

You can 
* fetch an external software container from a public repository URL and launch it on the fly (this includes Docker images),
* launch a software container image file that you have already downloaded to the filesystem,
* you may even be using a software container without realising it because some software on Bunya (`module load ...`) is provided seamlessly using containers.  

To make the magic happen you need to
* launch an interactive job an wait for that job to start running on a compute node,
* the apptainer/singularity command is automatically in your PATH (the apptainer command should just work on any _compute_ node)
* set environment variables that govern the location of where the container will store temporary files.<br> 
Specifically, you may run into /home quota trouble if you do not set the **SINGULARITY_CACHEDIR** and **SINGULARITY_TMPDIR** where you have sufficient space (such as `/scratch/user` or `/scratch/project`)
* provide a complete apptainer/singularity command line invocation including bind mounts.

Of course, you can also use software containers within a regular batch job, noting the points above about cache and tmp directories and bind mounts.

#### Where and how to build a software container

Singularity/Apptainer software containers do _not_ need to be built on systems where the user has system admin access. 
So, regular users are able to _build_ software containers on Bunya. 
There is, however, one complication. The GPFS filesystem that underpins your `/scratch` and `/home`, as well as `$TMPDIR`, does not support "sandbox" mode. Sandbox mode allows you to add additional functionality to a container created with just a rudimentary installation. The sandbox needs to be converted to a portable image file once it has been completely built. If you need to use sandbox mode on Bunya, please contact RCC Support. 

You can build your own on a suitable external system and bring it onto Bunya.

You cannot build a container on Bunya directly from a Dockerfile prescription. Instead, you will need to use the docker software to create a container image and upload it to a suitable repository. Then you will be able to "pull" a copy of it and it will be converted to apptainer format.

## Fair Share

Bunya employs [fair share](FairShare.md) to ensure that each user is able to use Bunya resources.

## Interactive jobs

### Do not run on the login nodes

>[!WARNING]
>Users are reminded that no computing task, no matter how quick or small, should be run on the login nodes. So no, the quick python or R or bash script or similar should NOT be just quickly run from the command line as it is so much more convenient. **All calculations, installations and file operations are required to be done on the compute nodes.**
>
>This includes software installations. Conda create, pip installs and R install.packages should be run via an interactive job not on the login nodes. Software installations using make and then make install (or cmake) especially are not suitable to be done on a login node. For these users should be careful choosing the correct architecture, see [here](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#how-to-build-your-own-software)
>
>Users can use interactive jobs which will give them that command line feel and flexibility and allow the use of graphical user interfaces. Users who need a Graphical User Interface (GUI) should consult the [onBunya User Guide](./OnDemand-Guide.md). 
>
>Users have access to a `debug` QoS for quick testing of new jobs and codes etc.
>
>Processes that should not be running on the login nodes may be terminated without explanation.

### Interactive jobs

User should use interactive jobs to do quick testing and if they need to use a graphical user interface (GUI) to run their calculations. This could include jupyter, spider, etc. 
Filesystem operations (e.g. housekeeping tasks, packing and unpacking data sets, copying data from/to RDM or scratch, pulling data from external sources) is much more efficient on a compute node compared with the login nodes.

The salloc is used to submit an interactive job and you should specify the required resources via the command line. IMPORTANT: Interactive jobs should be limited to a single node. Multinode jobs are required to be submitted as a batch job.

**Jobs need to request all resources they need or they will fail. This includes GPUs (default is zero) and walltime.** 

#### How do I launch an interactive job ?

**Use this full command line to create an interactive session on a compute node. Use the copy icon on the right hand side.**
<br>
```
salloc --nodes=1 --ntasks-per-node=1 --cpus-per-task=1 --mem=5G --job-name=CHANGE-ME --time=01:00:00 --partition=general --qos=debug --account=AccountString srun --export=PATH,TERM,HOME,LANG --pty /bin/bash -l
```

>[!WARNING]
>For interactive work, we recommend that you combine `salloc` and `srun`, as shown above, to ensure that your session switches to a Bunya compute node and does not remain on the login node.
><br><br>
>You can use the salloc, followed by separate srun commands, however _*every*_ command that you wish to run on the allocated compute node must be explicitly `srun`.  Otherwise, that processing will happen on your login node.
><br><br>
>In either case, once the walltime of the salloc has elapsed, the job will terminate and the control will return to your login node. In that case, any subsequent commands will run on the login node and will cause problems. Always confirm what node you are on, before running computations on Bunya. 

#### How can I confirm that I am running on a compute node ?

Your shell login prompt will usually include the name of the node. 
However, some people sometimes don't see that (notably when they use conda environments).

You can use the command<br>
`hostname`<br>
to check that you are on a compute node. If the command output includes `bunya1` or `bunya2` then you are still on a login node. <br> **Do not start your calculation, compile or environment install on a login node.* Make sure you are on a compute node. 

When an interactive job reaches the walltime, the job will terminate and your login session will return to the login node. Again, check your login prompt or use the `hostname` command to confirm you are on a compute node before doing work.

#### Which Partition and QoS ?

Please use `--partition=general` unless you need access to GPUs. The `general` partition has `epyc3` and `epyc4` architecture CPUs. The `--qos=debug` has a higher priority but has a walltime limit of 1 hour and limits number of jobs per user. Use `--qos=normal` to submit standard jobs. The `normal` QoS does not allow GPUs. 

#### What is my AccountString ?

Use the `groups` command to list your groups- Bunya Account Strings will begin a_ . Replace `AccountString` with your actual accounting group in the `--account=` option. This is the AccountString for your research or accounting group. All AccountStrings start with a_. Use the `groups` command to list your group memberships and grab the one that begins with `a_` characters.

#### What if I need a particular CPU type ?

To target an `epyc3` compute node add `--constraint=epyc3` to the `salloc` part. To target an `epyc4` compute node add `--constraint=epyc4` to the `salloc` part.

#### What about using a GUI ?

If you need to run a GUI then add the option `--x11` to the `salloc` part.

#### What about using a GPU interactively ?

For an interactive session on the `gpu_rocm` or `gpu_cuda`  partitions you will need to add `--gres=gpu:[type]:[number]` to the `salloc` request and use `--qos=gpu` instead of `--qos=normal`. It is important that you use a **`[type]`** to get the correct GPU card for your job.

To target a particular GPU RAM in the `gpu_cuda` partition, especially an A100 MIG slice add `--constraint=cuda10gb`, or `--constraint=cuda80gb` to target a card with the full GPU RAM to the `salloc` part.

See [here](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#available-partitions-and-nodes) for a full list of partitions, QoS, GPU types and other features.

This will log you onto a node. To run a job just type as you would usually do on the command line. As `srun` was already used in the above command there is no need to use `srun` to run your executables, it will just mess things up.

Once you are done type `exit` on the command line which will stop any processes still running and will release the allocation for the job.

Alternatively, if you use _just_ an `salloc` on the login node, then you _must_ use `srun` to run your command otherwise it will start running on login node and that is not fair on other users.



### Interactive MPI jobs only (for experts)

Instructions for **experts** who know what they are doing in terms of MPI and its usage can be found [here (for MPI experts only)](Expert-only-MPI-testing.md)


## Available partitions

The available partitions on Bunya are
```
general
gpu_rocm
gpu_cuda
gpu_sxm
gpu_viz
```
## Available Quality of Service (QoS)

```
normal
debug
mig
sxm
sdf
gpu
viz
```
<br>

## QoS use and limits

QoS are used to control access to resources and apply sustainable limits.<br> 

**Important:**<br>
mig requires the request of at least 1 MIG slice: gres=gpu:nvidia_a100_80gb_pcie_1g.10gb:1<br>
sxm requires the request of at least 1 H100:gres=gpu:h100:1<br>
viz for onBunya jobs only<br>
onBunya Accelerated Desktops with 2 or 3 GPUs will be submitted with the gpu QoS.<br>
gpu still requires that at least one GPU is requested for the job as the default for number of GPUs is zero.<br>


| QOS |  Partitions |  Access| Priority | All User Group limit | User limits |
|:---|:---|:---:|:---:|:---|:---|
|||||||
| normal | general | open | 10 | 20000 CPUs, <br> 200 T CPU memory | 1536 CPUs,<br> 16 T CPU memory,<br> 0 GPUs,<br> 5000 jobs submitted | 
| debug | general,<br> gpu_rocm,<br> gpu_cuda,<br> gpu_viz | open | 20 | none | 1 hour, <br> 1536 CPUs, <br> 16 T CPU memory, <br> 4 GPUs, <br> 2 jobs running, <br> 20 jobs submitted |
| gpu | gpu_rocm,<br> gpu_cuda,<br> gpu_viz | open | 10 | none | 256 CPUs, <br> 2 T of CPU memory, <br> 4 GPUs, <br> 4 jobs running, <br> 100 jobs submitted |
| mig | gpu_cuda | open | 10 | none | 441 CPUs, <br> 1932 GB CPU memory, <br> 21 GPUs, <br> 1000 jobs submitted |
| sxm | gpu_sxm | approved users | 10 | none | 192 CPUs, <br> 1 T CPU memory, <br> 4 GPUs, <br> 4 jobs running, <br> 50 jobs submitted |
|sdf | gpu_rocm| approved users | 10 | none | 256 CPUs, <br> 2 T CPU memory, <br> 8 GPUs |
| viz | general, <br> gpu_viz| onBunya only | 20 | none | 1 day,<br> 192 CPUs (96 CPU per job), <br> 500G per job, <br> 2 GPUs (1 GPU per job), <br> 2 running jobs, <br> 20 jobs submitted | 
<br>

## Available partitions and nodes

The available compute nodes on Bunya are listed in the table below. Please note while some feature the same CPU or GPU type, the available memory and/or number of CPUs or architecture can differ. Be mindful of this when requesting resources for jobs.

**Maximum walltimes**:<br>
general: 2 weeks (14 days, 336 hours)<br>
gpu_cuda, gpu_viz, gpu_rocm, gpu_sxm: 1 week (7 days, 168 hours)<br> 

**Default walltime for all partitons: 30 minutes**

**Default number of GPUs for all partitons: zero**

**gpu_viz** is used exclusively by onBunya. Users should not be submitting batch jobs via sbatch to the gpu_viz partition. The L40 and L40s GPUs are available through the gpu_cuda partition. <br>


| Partition | Hostnames |  Count |  CPU Memory (MB) per node| CPUS per node| FEATURES | GRES per node| Charge Multiplier|
|:---|:---|:---:|---:|:---:|:---|:---|---:|
| general | bun[006-008] | 3 | 4000000 | 192 | epyc3 | (null) | 1 |
| general | bun[009-067] | 59 | 2000000 | 192 | epyc3 | (null) | 1 |
| general| bun[083-115,126-143] | 51 | 1500000 | 192 | epyc4 | (null) | 1 |
|||||||||
| gpu_cuda | bun003 | 1 | 2000000 | 256 | epyc3,<br> cuda,<br> cuda80gb | gpu:a100:3 | 50 |
| gpu_cuda | bun[004-005] | 2 | 2000000 | 256 | epyc3,<br> cuda,<br> cuda10gb | gpu:nvidia_a100_80gb_pcie_1g.10gb:6, <br> gpu:nvidia_a100_80gb_pcie_2g.20gb:3, <br> gpu:nvidia_a100_80gb_pcie_3g.40gb:3| 6, <br> 12, <br> 24 |
| gpu_cuda | bun068 | 1 | 2000000 | 192 | epyc3,<br> cuda,<br> cuda80gb | gpu:a100:2 | 50 |
|||||||||
| gpu_cuda | bun[071-076,116] | 7 | 2000000 | 192 | epyc3,<br> cuda,<br> cuda80gb | gpu:h100:3 | 100 |
| gpu_sxm | bun[117-120] | 4 | 1000000 | 192 | xeonsp4,<br> cuda,<br> cuda80gb,<br> sxm | gpu:h100:4 | 100 |
|||||||||
| gpu_cuda <br> gpu_viz | bun[077-082] | 6 | 2000000 | 192 | epyc3,<br> cuda,<br> cuda48gb | gpu:l40:3 | 40 |
| gpu_cuda <br> gpu_viz | bun[124-125] | 2 | 750000 | 192 | epyc4,<br> cuda,<br> cuda48gb | gpu:l40s:3 | 42 |
| gpu_viz | bun[121-123] | 3 | 750000 | 192 | epyc4,<br> cuda | gpu:a16:12 | 6 |
|||||||||
| gpu_rocm | bun[001-002] | 2 | 500000 | 192 | epyc3,<br> rocm | gpu:mi210:2 | 50 |
| gpu_rocm | bun070 | 1 | 380000 | 64 | epyc4,<br> rocm | gpu:mi210:2 | 50 |
| gpu_rocm | bun145 | 1 | 2000000 | 128 | epyc4, <br> rocm | gpu:mi300x:8 | 100 |
| gpu_rocm | bun146 | 1 | 2000000 | 192 | epyc4, <br> rocm | gpu:mi300x:8 | 100 |

## Maximum CPU resources per GPU

>[!IMPORTANT] 
>Users should be mindful of the CPU resources per node when requesting GPU resources. Over requesting CPU resources such as the number of CPUs and CPU ram can unintentionally block other GPUs on the same node being used as the CPU resources of other jobs cannot be accommodated even if GPUs are still free. This can lead to unnecessary wait time for other users's jobs and might lead to GPU resources being left idle. Users should request the resources that their job needs to run and not just arbritary CPU resources or just always the same CPU resources. Users are required to check the resource utilisation of their jobs and adjust future job accordingly.
>Jobs that are found to not utilise the resources they have requested and are blocking free GPUs being used mayb be terminated.  

This table shows what are appropriate maximum CPU resource requests per GPU, depending on the GPU and GPU node.

| Partition | Hostnames |  Count | Max CPU Memory (MB) per GPU| Max CPUS per GPU | FEATURES | GPUs per node | multiplier per GPU|
|:---|:---|:---:|---:|:---:|:---|:---|---:|
| gpu_cuda | bun003 | 1 | 700000 | 86 | epyc3,<br> cuda,<br> cuda80gb | gpu:a100:3 | 50 |
| gpu_cuda | bun[004-005] | 2 | 180000 | 22 | epyc3,<br> cuda,<br> cuda10gb | gpu:nvidia_a100_80gb_pcie_1g.10gb:6, <br> gpu:nvidia_a100_80gb_pcie_2g.20gb:3, <br> gpu:nvidia_a100_80gb_pcie_3g.40gb:3| 6, <br> 12, <br> 24 |
| gpu_cuda | bun068 | 1 | 1000000 | 96 | epyc3,<br> cuda,<br> cuda80gb | gpu:a100:2 | 50 |
|||||||||
| gpu_cuda | bun[071-076,116] | 7 | 700000 | 64 | epyc3,<br> cuda,<br> cuda80gb | gpu:h100:3 | 100 |
| gpu_sxm | bun[117-120] | 4 | 250000 | 48 | xeonsp4,<br> cuda,<br> cuda80gb,<br> sxm | gpu:h100:4 | 100 |
|||||||||
| gpu_cuda <br> gpu_viz | bun[077-082] | 6 | 700000 | 64 | epyc3,<br> cuda,<br> cuda48gb | gpu:l40:3 | 40 |
| gpu_cuda <br> gpu_viz | bun[124-125] | 2 | 250000 | 64 | epyc4,<br> cuda,<br> cuda48gb | gpu:l40s:3 | 42 |
| gpu_viz | bun[121-123] | 3 | 64000 | 16 | epyc4,<br> cuda | gpu:a16:12 | 6 |
|||||||||
| gpu_rocm | bun[001-002] | 2 | 250000 | 96 | epyc3,<br> rocm | gpu:mi210:2 | 50 |
| gpu_rocm | bun070 | 1 | 190000 | 32 | epyc4,<br> rocm | gpu:mi210:2 | 50 |
| gpu_rocm | bun145 | 1 | 250000 | 16 | epyc4, <br> rocm | gpu:mi300x:8 | 100 |
| gpu_rocm | bun146 | 1 | 250000 | 16 | epyc4, <br> rocm | gpu:mi300x:8 | 100 |


<br>

## Slurm scripts

Users should keep in mind that Bunya has 96 cores (192 threads) per node. 96 cores (`--ntask-per-node=96`)  192 threads (`--cpu-per-task=192`)  is therefore the maximum a multi thread job can request. Please note not all calculations scale well with cores, so before requesting all 96/192 cores/threads **do some testing first**. 

The GPU nodes can have different nmbers of CPUs available. Users are reminded to check and request sensible CPU numbers with their GPU requests.

The Pawsey Centre has an excellent guide on how to [migrate from PBS to SLURM](https://pawsey.atlassian.net/wiki/spaces/US/pages/51925978/How+to+Migrate+from+PBS+Pro+to+Slurm). The Pawsey Centre also provides a good general overview of [job scheduling with Slurm](https://support.pawsey.org.au/documentation/display/US/Job+Scheduling) and [examples workflows](https://support.pawsey.org.au/documentation/display/US/Example+Workflows) like array jobs.

### How to submit a job

You would usually write a slurm script to subimit your jobs. Once you have a script you use `sbatch` to submit this script. For example if you have a script called `first-job-script` then you use<br>

`sbatch first-job-script`<br>

to submit the slurm script and your job.

**Jobs need to request all resources they need or they will fail. This includes GPUs (default is zero) and walltime.** 

Below are examples for single thread, single node but multiple threads, MPI, and array job submission scripts. 
The different request flags mean the following:
<br>
`#SBATCH --nodes=[number]` - how many nodes the job will use<br>
`#SBATCH --ntasks-per-node=[number]` - This is 1 for single thread jobs and multi thread jobs. This is 96 (or less if single node) for MPI jobs.<br>
`#SBATCH --ntasks=[number]` - total number of tasks of the job. Relevant to MPI jobs (it is usually 1 for non-MPI jobs) and should be set to the total number of tasks for the job (what you would use with the -np or -n option for mpirun). This should be used instead of requesting number of nodes and tasks per node to enable faster scheduling of MPI jobs.<br> 
`#SBATCH --ntasks-per-core=[number]` - maximum  ntasks on each core. Use with `--ntasks=[number]` for MPI jobs and set to `--ntasks-per-core=1`.
`#SBATCH --cpus-per-task=[number]` - This is 1 for single thread jobs, number of threads for multi thread jobs. `--cpus-per-task` can be undertstood as `OMP_NUM_THREADS`. Do not use for MPI jobs.<br>
`#SBATCH --hint nomultithread` - This option may help in situations where your parallelisation (single node multicore or hybrid OpenMP+MPI) is confused by the numbers of cores/threads.<br>
<br>
`#SBATCH --mem=[number M|G|T]` - RAM per job given in megabytes (M), gigabytes (G), or terabytes (T). The full memory of 1.5 TB r 2TB or 4TB is not available to jobs, therefore jobs asking for 1.5TB or 2TB or 4TB (1500G or 2000G or 4000G) will NOT run. Ask for `1500000M` to get the maximum on an `epyc4` standard node. Ask for `2000000M` to get the maximum memory on a `epyc3` standard node. Ask for `4000000M` to get the maximum memory on a high memory node. See note below why.<br>
`#SBATCH --mem-per-cpu=[number M|G|T]` - alternative to the request above, only relevant to MPI jobs.<br>
<br>
`#SBATCH --gres=gpu:[type]:[number]` - to request the use of GPU on a GPU node. Please see description of partitions above for the available types of GPUs<br>
`#SBATCH --time=[hours:minutes:seconds]` - time the job needs to complete. Partition limits: `general` = 336 hours (2 weeks), `gpu_rocm, gpu_cuda, gpu_sxm` = 168 hours (1 week).<br>
<br>
`#SBATCH --qos=[normal,gpu,debug,mig,sxm,sdf]` - to request a quality of service for the job.<br>
`#SBATCH -o filename` - filename where the standard output should go to. See `man sbatch` for filename templating options.<br>
`#SBATCH -e filename` - filename where the standard error should go to. See `man sbatch` for filename templating options.<br>
`#SBATCH -job-name=[Name]` - Name for the job that is seen in the queue<br>
<br>
`#SBATCH --account=[Name]` - AccountString for your research or accounting group. All AccountStrings start with `a_`. Use the `groups` command to list your groups<br>
<br>
`#SBATCH --constraint=[epyc3 or epyc4]` - to submit to a specific CPU architectures if required, needs to be applied with `--batch` below.<br>
`#SBATCH --batch=[epyc3 or epyc4]` - to submit to the a specific CPU architecture, needs to be applied with `--constraint` above.<br>
<br>
`#SBATCH --partition=general/gpu_rocm/gpu_cuda/gpu_sxm`<br>
<br>
`#SBATCH --array=[range]` - Indicates that this is an array job with range number of tasks. Range can be `0-999`. The maximum range value is 1000.<br>
<br>
`srun` - runs the executable using the resources you requested for this job. It will receive info on number of threads, memory, etc from Slurm. There is no need to specify them here.

See `man sbatch` and `man srun` for more options (use arrow keys to scroll up and down and `q` to quit)

***Default partition is general*** If you do not specify a partition when you submit you get the default partition. The default partition is `general` which is CPU only.  Important, the slurm defaults are usually not sufficient for most user jobs. If you want appropriate resources, you are required to request them.

***Standard outout and error***: Using the `SBATCH` options `-o` and `-e` with a `filename` in a script will result in the standard error and standard output file to appear as soon as the job starts to run. This behaviour is different to standard PBS behaviour on Tinaroo and FlashLite (unless you specified paths for those files there too) where the standard error, .e, and standard output, .o, files only appeared when the job was finished or had crashed.

***Default working directory***: In Slurm your job will start in the directory/folder you submitted from. This is different to PBS behaviour where your job started in your home directory. So on Bunya, using slurm, there is no need to change into the job directory, unless this is different to the directory you submitted from.

***$TMPDIR***: If your job produces temporary files during the calculation or if you need a space to write to that does not impact your quotas in `/home`, `/scratch/user` or `/scratch/project` then please use **$TMPDIR** during your calculations. **$TMPDIR** is automatically created at the start of a job and is then automatically deleted at the end of the job. It is therefore the best place to write temporary files (those not needed after the calculation is done) to. If you use **$TMPDIR** for output you wish to keep then please make sure you copy all needed files to a location in `/home`, `/scratch/user`, `/scratch/project` or `/QRISdata`. A big (all in one go) copy from **$TMPDIR** to `/QRISdata` (RDM) at the end of a job is possible.

***Note on maximum memory requests:*** The standard compute node has 2TB of physical memory available (or 4TB for the 3 high memory compute nodes). Not all of this can be given to jobs running on the compute node as the Linux operating system also needs resources. This is why the maximum requestable memory has been capped at 2000000MB for the standard compute nodes and 4000000MB for high memory compute nodes. 

So why is 2000000MB not the same as 2TB? 1024 MB = 1 GB and 1024 GB = 1 TB. This means 2000 GB = 2048000 MB which is larger than 2000000M which is set as the maximum available memory on a standard compute node.

***Accounting has now been switched on and will be enforced. Users cannot run jobs without a valid AccountString. Type `groups` on the command line to check if you have one. All valid AccountStrings start with `a_` and are all lower case letters. If you do not have a valid AccountString then please contact your supervisor. AccountStrings and access are managed by research groups and group leaders. Groups who wish to use Bunya are required to apply to set up a group with a valid AccountString. Only group leaders can apply to set up such a group. A PhD student or postdoc without their own funding and group should not apply. Applications can be made by contacting [rcc-support@uq.edu.au](mailto:rcc-support@uq.edu.au).***

### Simple script for CUDA GPUs.

```
#!/bin/bash --login
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=10G
#SBATCH --job-name=CHANGE-ME
#SBATCH --time=1:00:00
#SBATCH --qos=gpu
#SBATCH --partition=gpu_cuda
#SBATCH --gres=gpu:nvidia_a100_80gb_pcie_1g.10gb:1
#SBATCH --account=AccountString
#SBATCH -o slurm-%j.output
#SBATCH -e slurm-%j.error

module-loads-go-here

srun executable < input > output
```
For full A100 change to<br>
`#SBATCH --gres=gpu:a100:1`<br>

For H100 change to<br> 
`#SBATCH --gres=gpu:h100:1`<br>

For L40 change to<br> 
`#SBATCH --gres=gpu:l40:1`<br>

For L40s change to<br> 
`#SBATCH --gres=gpu:l40s:1`<br>


### Simple script for AMD ROCM GPUs.

**Nodes bun001, bun002, bun070, and bun145. These are AMD GPUs. You most likely will need to compile your own code or use a container to run on these.**

```
#!/bin/bash --login
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=10G
#SBATCH --job-name=CHANGE-ME
#SBATCH --time=1:00:00
#SBATCH --qos=gpu
#SBATCH --partition=gpu_rocm
#SBATCH --gres=gpu:mi210:1 #you can ask for up to 2 here
#SBATCH --account=AccountString
#SBATCH -o slurm-%j.output
#SBATCH -e slurm-%j.error

module-loads-go-here

srun executable < input > output
```
For Mi300x change to<br>
`#SBATCH --gres=gpu:mi300x:1`<br>
With `--qos=gpu` you can ask for up to 4<br>
With `--qos=sdf` you can ask for all 8<br>


### Simple script for CPUs and single node

```
#!/bin/bash --login
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=10G
#SBATCH --job-name=CHANGE-ME
#SBATCH --time=1:00:00
#SBATCH --qos=normal
#SBATCH --partition=general
#SBATCH --account=AccountString
#SBATCH -o slurm-%j.output
#SBATCH -e slurm-%j.error

module-loads-go-here

srun executable < input > output
```

To ask for more than 1 thread change the line

`#SBATCH --cpus-per-task=12`

To run over 12 threads for example.


You can target specific architectures like `epyc3` (phase 1) and `epyc4` (phase 2) by adding

```
#SBATCH --constraint=[epyc3 or epyc4]
#SBATCH --batch=[epyc3 or epyc4]
```


### Simple MPI script (using 192 cores, as an example). Using --ntasks will spread the job over multiple nodes where there is space.

```
#!/bin/bash --login
#SBATCH --ntasks=192
#SBATCH --ntasks-per-core=1
#SBATCH --mem-per-cpu=5G
#SBATCH --job-name=MPI-CHANGE-ME
#SBATCH --time=1:00:00
#SBATCH --qos=normal
#SBATCH --partition=general
#SBATCH --account=AccountString
#SBATCH -o slurm-%j.output
#SBATCH -e slurm-%j.error

module-loads-go-here

srun executable < input > output
```

You can target specific architectures like `epyc3` (phase 1) and `epyc4` (phase 2) by adding

```
#SBATCH --constraint=[epyc3 or epyc4]
#SBATCH --batch=[epyc3 or epyc4]
```

### Job Arrays

Here is one example of an array job script with 5 array tasks. Important: Request resources for a single task and not resources for all together.

```
#!/bin/bash --login
#SBATCH --job-name=array-CHANGE-ME
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=5G
#SBATCH --time=00:01:00
#SBATCH --qos=normal
#SBATCH --partition=general
#SBATCH --account=AccountString
#SBATCH --output=test_array_%A_%a.out
#SBATCH --array=1-5

module-loads-go-here

srun executable < input > output
```

Useful variables for array jobs

`$SLURM_ARRAY_JOB_ID` = Job array's master job ID number.<br>
`$SLURM_ARRAY_TASK_COUNT` = Total number of tasks in a job array.<br>
`$SLURM_ARRAY_TASK_ID` = Job array ID (index) number.


You can target specific architectures like `epyc3` (phase 1) and `epyc4` (phase 2) by adding

```
#SBATCH --constraint=[epyc3 or epyc4]
#SBATCH --batch=[epyc3 or epyc4]
``````

### How to manage your jobs and cluster activity in SLURM

#### To list _only_ your jobs
`squeue -u YourUsername`<br>
`squeue -u $USER`<br>
`squeue --me`<br>

#### Some formatting ideas for more detailed squeue reports

Here are some other useful additions to the squeue command. For information on what all these means please consult the man pages.

```
squeue -o "%.18i %.9P %.8j %.8u %.8T %.10M %.9l %.6D %.10a %.4c %R"
JOBID  PARTITION  NAME  USER  STATE  TIME TIME_LIMIT NODES  ACCOUNT  MIN_CPU  NODELIST(or REASON)
```

```
squeue -o "%12i %7q %.9P %.20j %.10u %.2t %.11M %.4D %.4C %.14b %8m %16R %18p %10B %.10L" 
JOBID QOS PARTITION NAME USER STATE TIME NODE CPUS TRES_PER_NODE MIN_MEMORY NODELIST(REASON) PRIORITY EXEC_HOST TIME_LEFT
```
```
#One for the MPI users, perhaps!
squeue -o "%.7i %.9P %.8j %.8u %.2t %.10M %.6D %C"
JOBID PARTITION     NAME     USER ST       TIME  NODES CPUS
```

#### When you are wondering why your job has not started

##### Check the REASON in your squeue output

Checking the REASON field of the squeue output should provide you with some clue.
The manual page for the squeue command lists the most commonly encountered reasons.
They can be found in the "JOB REASON CODES" section of the `man squeue` command output or online [here](https://slurm.schedmd.com/squeue.html#SECTION_JOB-REASON-CODES).
A full list of job reasons can be found on [this web page](https://slurm.schedmd.com/resource_limits.html#reasons) 

##### QOSGrpCpuLimit or QOSGrpMemLimit

[20241024] A recent change was made to the batch system configuration to accommodate the Bunya Phase 3 hardware and associated workloads. It makes greater use of the QOS feature of SLURM. 
So you may now see the REASON given as "QOSGrpCpuLimit" or perhaps "QOSGrpMemLimit" for why your job is queued and not running. 
When it says that it means that Bunya is currently very busy and there is no available space for your job, at the moment. Previously it would have said something to the effect of Resources are unavailable.

Your jobs _will_ eventually start, if, you leave them in the queue!

##### Check the sinfo output for a status report of Bunya nodes

The sinfo command is used to obtain information about the actual nodes.<br>
You can request the report for a single or all partitions.<br>
Some of the more commonly seen values for the STATE are: 
* idle => nothing running so completely empty
* mix => running jobs but have space available
* drain or drng => drained or draining ... will finish current jobs and await maintenance work
* alloc => fully allocated so no space available
<br>
Here's a snippet for GPU partitions and nodes. So 3 CUDA nodes and 2 VIZ nodes are empty.

```
PARTITION  AVAIL  TIMELIMIT  NODES  STATE NODELIST
gpu_cuda      up 7-00:00:00     14    mix bun[003-004,068,071-079,082,116]
gpu_cuda      up 7-00:00:00      3   idle bun[005,080-081]
gpu_viz       up 7-00:00:00      4    mix bun[077-079,082]
gpu_viz       up 7-00:00:00      2   idle bun[080-081]
```

Here some useful examples.

```
sinfo -o "%n %e %m %a %c %C"
which yields
HOSTNAMES FREE_MEM MEMORY AVAIL CPUS CPUS(A/I/O/T)
```

`sinfo -O Partition,NodeList,Nodes,Gres,CPUs`<br>

```
sinfo -o "%.P %.5a %.10l %.6D %.6t %N %.C %.E %.g %.G %.m"
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST CPUS(A/I/O/T) REASON GROUPS GRES MEMORY
```

#### How to know what resources are actually being utilised by a job?

It is also very important that your jobs do not occupy valuable HPC resources and _not_ utilise them.
The fairshare system calculates your usage based on the resources you requested.
If you order a lot of food, but you don't eat it all, then you still pay for the food you ordered.
HPC's don't have a mechanism like doggy bags ;-)

The fairshare system will account for your usage based on the resources (CPU and/or MEM) you requested even if you did not consume them all. That is because no one else could used those resources while your job was running. A job that finishes earlier than the requested walltime does get charged less.

We often don't know in advance how much resource a set of jobs may require. 
You may have some idea based on calculations you have performed on a workstation or other HPC cluster.
Obviously if your software cannot utilised a GPU resource you would never request it.
But if you have CPU code that is expected to run faster on a single node in shared memory (OpenMP) mode, or on multiple nodes in message passing interface (MPI) mode, then you should be certain that you are getting the performance gains that you expect.

To prevent users unintentionally reducing their fair share RCC is starting to automatically delete jobs that leave GPU resources idle. The parameters for automatic deletion are:<br>

* GPU job
* Runtime of at least 24 hour
* At least 3 hours of walltime left
* Idle GPU resources for the last 4 hours


##### Jobstats

You can use the `jobstats` module to check utilisation of running and completed jobs. It will show max CPU, max CPU Ram, average GPU, and max GPU Ram utilisation over the elapsed runtime of the job. Jobstats provides a direct link in the comments to a graphical dashboard in onBunya to show resource utilistaion for whole runtime interval. Jobstats works on running and finihsed jobs. 

```
module load jobstats
jobstats JobID
```


##### A running job

You are able to access any node that is running a job that belongs to you. 

The `squeue --me` command will tell you which node is running your job.
You will need to set up SSH public/private keys and authorized_keys to allow you to easily ssh to any compute node. 
Refer to [this section](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#accessing-compute-nodes-from-login-nodes), above, for how to setup SSH keypairs for internal connections within Bunya.

Once logged in to the node that is running your job you can use the `top -c -u $USER` command and note the %CPU and RES (memory) values for your processes.<br>
The performance of jobs running on NVIDIA GPUs can be monitored using the /usr/bin/nvidia-smi command once you are logged into the node running your job..

##### Cancelling a job

If you see that your job is not performing as expected, or is not properly utilising the resources you requested, then you should cancel the job. 

Use the *`scancel`* command to cancel the job. You can cancle an individaul job or job array element, or an entire job array.

Before resubmitting the job, review the job resource request and job inputs and code.

##### Your completed jobs, using sacct

The `sacct` command can be used to report CPU and Memory utilisation by a completed job.
```
sacct -p  -a -S now-48hours --format JobID,User,Group,State,Cluster,AllocCPUS,REQMEM,TotalCPU,Elapsed,MaxRSS,ExitCode,NNodes,NodeList,NTasks -u $USER
```
yields these metrics
```
|JobID|User|Group|State|Cluster|AllocCPUS|ReqMem|TotalCPU|Elapsed|MaxRSS|ExitCode|NNodes|NodeList|NTasks|
```
Notes:
* Each job will result in three of slightly different lines of output. 
* The requested memory is in the first line and the MaxRSS value is in the second line of the three lines for each job.
* Without specifying the start time (using `-S now-48hours`) for the report, sacct will report just your jobs for today (i.e. since midnight)
* You can use the `-j JobID` option to generate a report for a single job. 

##### Your completed jobs, using seff

The perl utility script /usr/local/bin/seff will generate a brief more readable report of the total resource utilisation (CPU and MEM). It does not report on GPU utilisation.
```
seff JobID
```

