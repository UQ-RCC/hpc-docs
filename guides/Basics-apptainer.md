# The Apptainer Basics

**EARLY DRAFT**
  
## What is a software container?


## Why is some software provided this way on Bunya?

## What is apptainer

## Gotchas

- The apptainer software is _NOT_ installed on login nodes.
- The default locations for container caches are in /home and this can quickly exceed your GB quota.
- Building a sandbox container can also blow your file count quota in /scratch so consider building sandboxes in /home or $TMPDIR.

## What storage can I access from within the container ?
  
A software container can automatically access `/home` and `/scratch/user` because natively you will most often run the container as your default username and group.
- To access your RDM collection, you will need to switch your group from your standard group to the RW group associated with the collection storage allocation (e.g. if qris-uq, then `newgrp Q9999RW`).
- If you need to access your `/scratch/project`, switch your group from your standard group to the access group associated with the `/scratch/project` space.
  
  
## What are the steps

- build a container (usually from a .def definition file)
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
|1|create a container image outright|`apptainer build myContainer.sif myContainer.def`|
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

For more info about apptainer consult the manual page and online resources.
