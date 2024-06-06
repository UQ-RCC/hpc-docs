# Where should my data and software go on Bunya

Bunya has several spaces users have access to to keep their data and software.

### Spaces available by default for every user

The spaces below are individual spaces. This means, by default, they are only accessible by the user who this space belongs to. These spaces **should NOT be shared with any other users**. If a shared space is required please see further below in the section on shared spaces.

#### `/home/username` 
* Every user has a home directory. This is where a user lands when they login.
* Quotas are *50GB and 1 million files*.
* The home directory should be used to install software, such as conda, python and R environments, scripts, and other software installed by `make` and `make install`, etc.
* The home directory should **not** be used for data and output from calculations. The reason for this is that if it goes over one of the quotas (space of files) a user can effectively lock themsleves out of their account if they do not clean up (get back under quota) quickly. 
* The home directory is **not backed up**.

#### `/scratch/user/username`
* Every user has a directory in `/scratch/user`.
* Quotas are *150GB and 100,000 files*.
* The user scratch directory should be used to keep input and output of calculations.
* The user scratch directory can also be used to install software.
* The scratch user directory is **not backed up**.

### Checking quotas and usage in /home and /scratch

Users can use the command `rquota` on Bunya to check their current quotas and usage. It provides quotas and usage for `/home`, `/scratch/user` and `/scratch/project` (more information below) they have access too.

### Shared spaces, often require an application

#### `/scratch/project`

Scratch projects are shared spaces in `/scratch` that provide more space and space that is shared by members of a group.

* Apply for a scratch project by sending a request to rcc-support@uq.edu.au and you will then be send the link to the application form.
* Scratch projects should be used to install software that needs to be shared.
* Scratch projects can be used to share data sets and output that multiple users need access to during their calculations.
* The scratch project directory is **not backed up**.


#### `/QRISdata`

RDM storage records, where users selected that the data should be available on HPC when they have applied for the RDM storage record (it cannot be changed afterwards), are automatically available on Bunya in `/QRISdata/QNNNN`, where `QNNNN` is the storage record number and can be found as part of the short identifier for the RDM storage record.


* `/QRISdata/QNNNN` are shared spaces with default quotas of *1TB and 1 million files*. This can be increased by applying for more storage via the [RDM portal](https://rdm.uq.edu.au/).
* RHD students who have dual credentials (staff and student) may need to add the other credential as a collaborator. For example, if your RDM was created with your student account, then you will need to add your staff account as a collaborator if you need access to it from the staff credentials. You manage collaborators on your RDM via the [RDM portal](https://rdm.uq.edu.au/).
* Use `ls /QRISdata/QNNNN/` (the `/` at the end is important) or `cd /QRISdata/QNNNN` to see the RDM storage record. Due to the automount the RDM storage record needs to be used to be seen.
* Users are **not allowed** to submit jobs (type `sbatch` or `salloc`) from a directory in `/QRISdata`. 
* Jobs should not do multiple reads or writes from or to a directory in `/QRISdata` a calculations. So standard output should not be written to `/QRISdata`. A once off read of input at the start and a once off write at the end is permitted. However, the general data workflow should be using `/scratch` for input and output of calculations.
* Software should not be installed in `/QRISdata` as accessing software is also continuously accessing `/QRISdata` which is not permitted.
* Do not unpack archives or tar files directly in `/QRISdata`, unpack these into a directory in `/scratch`
* Do not move directories with many files to `/QRISdata`, tar or archive these first as lots of (small) files can cause problems (not just for you but also others).

##### How `/QRISdata` works

The `/QRISdata` filesystem provides access from Bunya to UQ RDM collections (as well as a smaller number of collections that predate UQ RDM).

The storage technology behind `/QRISdata` consists of multiple layers of storage, and software that manages the copies of your data within those multiple layers. There are also active links to other caches at St Lucia campus that allow you to drag and drop your file onto the St Lucia R:\ drive and have it appear automatically at the remote computer centre that houses Bunya and the RDM Q collections.

|Layer|Purpose|Response Time|
|:----|:------|:------------|
|GPFS Cache|Used for intersite transfers and is mounted onto Bunya HPC|Immediate once mounted onto Bunya|
|Zero Watt Storage (ZWS)|Disk drives that operate like tapes. Only powered on when required.|<1 minute to activate a read from off|
|Robotic Tape Silo|Deep archive copies|Can take several minutes to commence reading|

The hierarchical storage management (HSM) software will move files downwards when they are not in active use in the top layer.
If a file is required, but is not in the top layer, then it will be recalled from ZWS, or tape and copied into place on the GPFS Cache layer.

##### How can I check if my files are in the top layer?

_On a compute node via an onBunya or interactive batch job_

Use `ls -salh FILEPATH`

The output contains the size-occupied-on-disk in the first column and the actual-size in column 6

```
#This one is in the GPFS cache layer (size on disk matches actual size)
[uqdgree5@bun104 Q0837]$ ls -salh Training.tar
367M -rw-r--r--+ 1 uqdgree5 Q0837RW 367M Oct 30  2023 Training.tar

#This one is in the GPFS cache layer too but the size on disk is actually bigger because files occupy at least one block (512)
[uqdgree5@bun104 Q0837]$ ls -salh Readme.md
512 -rw-rw----+ 1 Q0837 Q0837RW 1 Sep 13  2023 Readme.md

#This one is not in GPFS cache (zero on disk but the actual filesize is 1.7MB)
[uqdgree5@bun104 Q0837]$ ls -salh .LDAUtype1.tgz
0 -rw-rw----+ 1 Q0837 Q0837RW 1.7M Dec 16  2019 .LDAUtype1.tgz

[uqdgree5@bun104 Q0837]$

```


##### How can I force a recall of my file from the lower layer(s)?

_On a compute node via an onBunya or interactive batch job_

Use `/usr/local/bin/recall_medici FILEPATH`
Wildcards are also supported.

The `recall_medici` command is also available on data.qriscloud.org.au if you don't have access to Bunya.
