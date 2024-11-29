# The Apptainer Basics

**TO BE COMPLETED**

David Green 28/11/2024
  
## What is a software container?
Software containers is a generic technology term. It provides a mechanism for different operating systems and software that are not available in the host operating system so they can be used safely on the HPC platform. Software containers can be built from a "recipe" or downloaded as pre-built images, often as a stack that is assembled on the fly.

The names Docker, Shifter, Singularity/Apptainer are like different "brands" that support software containers.



## Why is some software provided this way on Bunya?

There are several reasons for supporting the use of software containers on Bunya: 
* Software container technology provides a mechanism for us to support software that is not able to be run natively on the Bunya operating system.
* Software containers can be created offsite and brought onto Bunya and they should, for the most part, _just work_.
* Software containers can be built from offsite definition files and other build mechanisms if you require specific versions.

## What is apptainer

Bunya uses [*Apptainer*](https://apptainer.org/docs/user/latest/introduction.html). Apptainer was created when Singularity was rebranded when it joined the Linux Foundation. Currently, the version of Apptainer installed on Bunya is version 1.3.3-1.el8.

## How is apptainer provided on Bunya

* Apptainer is installed into the operating system on every compute node.
* Apptainer is _not_ installed on the Bunya login nodes.
* You must use an interactive job via the batch system (or an [onBunya](http://bunya-ondemand.rcc.uq.edu.au/) session) to be able to reach compute nodes and use apptainer.
* You do *not* need to load a software module to use the apptainer command.

## Gotchas

- The apptainer software is _NOT_ installed on login nodes.
- The default locations for container caches are in /home and this can quickly exceed your GB quota.<br> 
Specifically, you may need to set the **APPTAINER_CACHEDIR** and **APPTAINER_TMPDIR** to a location where you have sufficient space (such as `/scratch/user` , `/scratch/project` or `$TMPDIR`)
- Building a sandbox container can also consume your file count quota in `/scratch`.<br>Consider building sandboxes in `/home` or `$TMPDIR`.

## What storage can I access from within the container?
  
A software container can automatically access `/home` and `/scratch/user`.<br>This is because you will most often run the container as your default username and group.
- To access your RDM collection, you will need to switch your group from your standard group to the RW group associated with the collection storage allocation (e.g. if qris-uq, then `newgrp Q9999RW`).
- If you need to access your `/scratch/project`,<br>switch your group from your standard group to the access group associated with the `/scratch/project` space.
  
  
## What are the steps

- build or pull a container<br>We usually build from a .def definition file. A .def file can be a local file or can be online.<br>The pull can be used to download a ready-to-use software container from an external repository.
- run/exec/shell the container

### Building a container on Bunya

- if the definition file is complete for what you need then you can build it directly as an image file.
- if not then you can 
  - build in "sandbox mode", 
  - customise your container, 
  - and convert it to a standalone image.

## Using apptainer - 7 basic container operations

||Operation|Command|
|:-:|:------|:--|
|1a|create a container image outright|`apptainer build myContainer.sif myContainer.def`|
|1b|pull a container image|`apptainer pull ... `|
|2|create a sandbox|`apptainer build --sandbox myContainer.sandbox myContainer.def`|
|3|update the sandbox|`apptainer shell --writable myContainer.sandbox`|
|4|convert the sandbox to a standalone image|`apptainer build myContainer.sif myContainer.sandbox`|
|5|start a shell interface in the container|`apptainer shell myContainer.sif`|
|6|run the default action for the container|`apptainer run myContainer.sif`|
|7|exec an arbitrary action using the container|`apptainer exec myContainer.sif  someLinuxCommand`|


## Sample Session

```

Example 

```


## More Info
QCIF have notes on their training github (details to follow)
For more info about apptainer consult the manual page and online resources.
