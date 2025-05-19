# Where should my data and software go on Bunya

Bunya has several spaces users have access to to keep their data and software. These spaces are subject to the [Bunya User Data Spaces Operational Procedures](../policy/Bunya-User-Data-Spaces-Operational-Procedure.md).

### Spaces available by default for every user

The spaces below are individual spaces. This means, by default, they are only accessible by the user who this space belongs to. These spaces **should NOT be shared with any other users**. If a shared space is required please see further below in the section on shared spaces.

#### `/home/username` 
* Every user has a home directory. This is where a user lands when they login.
* The home directory of a new user is created when the user logs in for the very first time via ssh. onBunya login will **not** create a user's home directory.
* Quotas are *50GB and 1 million files*.
* Quotas on a user's home directory will not be increased.
* The home directory should be used to install software, such as conda, python and R environments, scripts, and other software installed by `make` and `make install`, etc.
* The home directory should **not** be used for data and output from calculations. The reason for this is that if it goes over one of the quotas (space or files) a user can effectively lock themsleves out of their account if they do not clean up (get back under quota) quickly. 
* The home directory is **not backed up**.
* The home directory **must not** be shared with other users.

#### `/scratch/user/username`
* Every user has a directory in `/scratch/user`.
* Quotas are *300GB and 1 million files*.
* The 300GB quota can be exceeded up to 5TB but only up to 2 weeks. The quota has to fall below 300GB within the 2 weeks period or the user can no longer write to `scratch/user`.
* Quotas in a user's `/scratch/user` directory may be increased.
* The scratch user directory should be used to keep input and output of calculations.
* The scratch user directory may also be used to install software.
* The scratch user directory is **not backed up**.
* Old files might be auto deleted
* The scratch user directory **must not** be shared with other users.

Users can use the command `rquota` on Bunya to check their current quotas and usage. It provides quotas and usage for `/home`, `/scratch/user` and `/scratch/project` (more information below) they have access too.

Users can use the command 
```
/usr/lpp/mmfs/bin/mmlsquota -u $USER --block-size=auto scratch:user
```
to check on their quotas and grace period in `/scratch/user`. 

#### `$TMPDIR`

* `$TMPDIR` is created automatically for each Slurm job and is then automatically deleted once the Slurm job finishes. It is the ideal place for temporary files of jobs.
* `$TMPDIR` currently provides upto 10TB (soft limit) and 11TB (hard limit) of temporary space for upto 10,485,760 (soft limit) and 11,534,336 (hard limit) files. These limits apply to the _aggregate_ across all running jobs _for each user_. 
* `$TMPDIR` is pre-set and unique for each running job. Do not create your own `$TMPDIR` or overwrite it with something else in your scripts.
* `$TMPDIR` does not count towards user quotas in `/home` or `/scratch/user` or project quotas in `/scratch/project`.
* `$TMPDIR` is not `/scratch/user`.
* `$TMPDIR` is not `/tmp`.
* `$TMPDIR` is recommended if calculations produce a very large amount of (often very small) files.
* Software that allows a flag or option to set a *temporary* or *scratch* directory should always use `$TMPDIR` and ***NOT*** `/tmp`.
* To use `$TMPDIR` for software that does not allow to set a temporary/scratch directory, change to `$TMPDIR` (`cd $TMPDIR`), then copy all required input files to `$TMPDIR` or use the full path to point to input files in `/scratch` or `/home` or `/QRISdata` (for `/QRISdata` restrictions apply, see below). After the calculation copy all ouput needed to `/scratch` or `/QRISdata` (see below for restrictions on `/QRISdata`) and make sure to tar and/or zip output if required. This will need to be done in your Slurm submit script.

  ```
  cd $TMPDIR
  cp input-files .
  srun ...
  cp output-files /scratch/.../. (or /QRISdata/.../.)
  
  ```

### Shared spaces, often require an application

#### `/scratch/opendata`

The opendata space is a read-only space to house data sets and models. Current data includes, GTDB, BLAST, Kraken, CheckM2, SingleM, nuScens, nuScenes-C, huggingface, ollama, gguf, and many more.

Users are required to check if the data they need is already housed in `/scratch/opendata` or could be housed there before requesting an increase to their `/scratch/user` space or scratch project. 

If data is not yet available in `/scratch/opendata` users can submit a request for data to be installed there.


#### `/scratch/project`

Scratch projects are shared spaces in `/scratch` that provide more space and space that is shared by members of a group.

* Apply for a scratch project by sending a request to rcc-support@uq.edu.au and you will then be send the link to the application form.
* Scratch projects may be used to install software that needs to be shared but applying for space in`/sw` is preferred.
* Scratch projects can be used to share data sets and output that multiple users need access to during their calculations.
* Scratch projects should not be used to provide additional scratch space for single users. For single users the quotas in `/scratch/user` can be increased. 
* The scratch project directory is **not backed up**.
* Old files might be auto deleted

#### How scratch projects work

Scratch projects require an access group. This can be an RDM storeage record access group (QNNNN) or a specific access group created by RCC for the scratch project. Users, not RCC, manage the access groups either via the [RDM portal](https://rdm.uq.edu.au/) for QNNNN groups, or via the [QRIScloud Portal](https://www.qriscloud.org.au/). 

For RDM storage record access groups (QNNNN) the RDM storage record owner add users as collaborators to the RDM storeage recrod via the [RDM portal](https://rdm.uq.edu.au/). 
For QRIScloud access groups, the group owner or administrator needs to go to the [QRIScloud Portal](https://www.qriscloud.org.au/) and click on *Account* to log in. Then they need to go to *Services Dashboard* and there look under *Groups* for the respective *Scratch Project group* and click on the link. This page outlines how to add and remove users from the access group for the proejct.

New users added either way will have to wait for this to take affect as permissions set in the [RDM portal](https://rdm.uq.edu.au/) need to be propagated to Bunya. In both case user should create a new login to Bunya to have new groups available in their environment. Users can check which groups they belong to by typing the command `groups` on Bunya.

Users in the access group who also have access to Bunya will have access to the scratch project on Bunya. They have `read-write` access to the scratch project directory. However, directories and files created by other scratch project members in the scratch project directories are only readable (and executable) but not writable (cannot be deleted for files, cannot be written to for directories) to others.

In the below example:<br> 
* `user-2` can change into `directory-1` but they will not be able to write to `directory-1` or delete files in `directory-1`<br>
* `user-1` can change into `directory-2` and can write to `directory-2` and delete files in `directory-2`<br>
* Only `user-1` can delete or change `file-1`<br>
* `user-1` and `user-2` can delete or change `file-2`<br>
* Only `user-1` change delete or change `executable-1`<br>
* `user-1` and `user-2` change delete or change `executable-2`<br>

* To make `directory-1` writable to other users than `user-1`, `user-1` needs to run

`chmod -R g+w directory-1`<br>
where `-R` means that this is run recursively for all subdirectories and files<br>
`g+w` adds **w**rite permissions to the **g**roup.


```
drwxr-sr-x.  2 user-1 Project_Access_Group        4K Feb  1 19:08 directory-1
drwxrwsr-x.  2 user-2 Project_Access_Group        4K Oct  9 2023  directory-2
-rw-r--r--.  1 user-1 Project_Access_Group        6M Mar 25 13:54 file-1
-rw-rw-r--.  1 user-2 Project_Access_Group        6M Mar 25 13:54 file-2
-rwxr-xr-x.  1 user-1 Project_Access_Group        6M Mar  8 14:01 executable-1
-rwxrwxr-x.  1 user-2 Project_Access_Group        6M Mar  8 14:01 executable-2
```


#### `/QRISdata`

The [RDM User Guides](https://guides.library.uq.edu.au/for-researchers/uq-research-data-manager) provide a lot of information about RDM research records and RDM storage records and how to use and administer these.

RDM storage records, where users selected that the data should be available on HPC when they have applied for the RDM storage record (it cannot be changed afterwards), are automatically available on Bunya in `/QRISdata/QNNNN`, where `QNNNN` is the storage record number and can be found as part of the short identifier for the RDM storage record.


* `/QRISdata/QNNNN` are shared spaces with default quotas of *1TB and 1 million files*. This can be increased by applying for more storage via the [RDM portal](https://rdm.uq.edu.au/).
* RHD students who have dual credentials (staff and student) may need to add the other credential as a collaborator. For example, if your RDM was created with your student account, then you will need to add your staff account as a collaborator if you need access to it from the staff credentials. You manage collaborators on your RDM via the [RDM portal](https://rdm.uq.edu.au/).
* Use `ls /QRISdata/QNNNN/` (the `/` at the end is important) or `cd /QRISdata/QNNNN` to see the RDM storage record. Due to the automount the RDM storage record needs to be used to be seen.
* Users are **not allowed** to submit jobs (type `sbatch` or `salloc`) from a directory in `/QRISdata`. 
* Jobs should not do multiple reads or writes from or to a directory in `/QRISdata` during a calculations. So standard output should not be written to `/QRISdata`. A once off read of input at the start and a once off write at the end is permitted. However, the general data workflow should be using `/scratch` for input and output of calculations.
* Software should not be installed in `/QRISdata` as accessing software is also continuously accessing `/QRISdata` which is not permitted.
* Do not unpack archives or tar files directly in `/QRISdata`, unpack these into a directory in `/scratch`
* Do not move directories with many files to `/QRISdata`, tar or archive these first as lots of (small) files can cause problems (not just for you but also others).

#### How `/QRISdata` works

The `/QRISdata` filesystem provides access from Bunya to UQ RDM collections (as well as a smaller number of collections that predate UQ RDM).

The storage technology behind `/QRISdata` consists of multiple layers of storage, and software that manages the copies of your data within those multiple layers. There are also active links to other caches at St Lucia campus that allow you to drag and drop your file onto the St Lucia R:\ drive and have it appear automatically at the remote computer centre that houses Bunya and the RDM Q collections.

|Layer|Purpose|Response Time|
|:----|:------|:------------|
|GPFS Cache|Used for intersite transfers and is mounted onto Bunya HPC|Immediate once mounted onto Bunya|
|Zero Watt Storage (ZWS)|Disk drives that operate like tapes. Only powered on when required.|<1 minute to activate a read from off|
|Robotic Tape Silo|Deep archive copies|Can take several minutes to commence reading|

The hierarchical storage management (HSM) software will move files downwards when they are not in active use in the top layer.
If a file is required, but is not in the top layer, then it will be recalled from ZWS, or tape and copied into place on the GPFS Cache layer.

#### How can I check if my files are in the top layer?

_On a compute node via an onBunya or interactive batch job_

Use `ls -salh FILEPATH`

The output contains the size-occupied-on-disk in the first column and the actual-size in column 6

```
#This one is in the GPFS cache layer (size on disk matches actual size)
[uquser@bun104 Q0837]$ ls -salh Training.tar
367M -rw-r--r--+ 1 uquser   Q0837RW 367M Oct 30  2023 Training.tar

#This one is in the GPFS cache layer too but the size on disk is actually bigger because files occupy at least one block (512)
[uquser@bun104 Q0837]$ ls -salh Readme.md
512 -rw-rw----+ 1 Q0837 Q0837RW 1 Sep 13  2023 Readme.md

#This one is not in GPFS cache (zero on disk but the actual filesize is 1.7MB)
[uquser@bun104 Q0837]$ ls -salh .LDAUtype1.tgz
0 -rw-rw----+ 1 Q0837 Q0837RW 1.7M Dec 16  2019 .LDAUtype1.tgz
```


#### How can I force a recall of my file from the lower layer(s)?

_On a compute node via an onBunya session or interactive batch job_

Use the `recall_medici` command. That command should be in your standard PATH, but in case it isn't, you can copy it completely using the icon on the right side of this code box:
```
/usr/local/bin/recall_medici FILEPATH
```
Replace FILEPATH with the name of the file(s) you wish to retrieve. Wildcards are also supported so you can retrieve the files in a folder.

The `recall_medici` command is also available on data.qriscloud.org.au if you don't have access to Bunya.

#### Why does it sometimes take longer to connect to my RDM from Bunya?

At a time between 20 past and 40 past the hour at the hours of  08, 12, 16, and 22,
access to the RDMs from Bunya can be delayed. It happens while the service access controls are being updated. Access can appear non-responsive for a few minutes. Best to wait 5 minutes and try again.


