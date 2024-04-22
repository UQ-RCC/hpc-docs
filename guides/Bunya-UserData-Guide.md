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

### Checking quotas and usage in /home and /scratch/user

Users can use the command `rquota` on Bunya to check their current quotas and usage. It provides quotas and usage for `/home`, `/scratch/user` and `/scratch/project` (more information below) they have access too.

### Shared spaces, often require an application

#### `/scratch/project`

Scratch projects are shared spaces in `/scratch` that provide more space and space that is shared by members of a group.

* Apply for a scratch project by sending a request to rcc-support@uq.edu.au and you will then be send the link to the application form.
* Scratch projects should be used to install software that needs to be shared.
* Scratch projects can be used to share data sets and output that multiple users need access to during their calculations.
* The scratch project directory is **not backed up**.


#### `/QRISdata`

RDM storage records, where users have selceted that the data should be available on HPC when they have applied for the RDM storage record (it cannot be changed afterwards), are automatically availble on Bunya in `/QRISdata/QNNNN`, where `QNNNN` is the storage record number and can be found as part of the short identifier for the RDM storage record.


* `/QRISdata/QNNNN` are shared spaces with default quotas of *1TB and 1 million files*. This can be increased by applying for more storage via the [RDM portal](https://rdm.uq.edu.au/).
* Use `ls /QRISdata/QNNNN/` (the `/` at the end is important) or `cd /QRISdata/QNNNN` to see the RDM storage record. Due to the automount the RDM storage record needs to be used to be seen.
* Users are **not allowed** to submit jobs (type `sbatch` or `salloc`) from a directory in `/QRISdata`. 
* Jobs should not do multiple reads or writes from or to a directory in `/QRISdata` a calculations. So standard output should not be written to `/QRISdata`. A once off read of input at the start and a once off write at the end is permitted. However, the general data workflow should be using `/scratch` for input and output of calculations.
* Software should not be installed in `/QRISdata` as accessing software is also continuously accessing `/QRISdata` which is not permitted.
* Do not unpack archives or tar files directly in `/QRISdata`, unpack these into a directory in `/scratch`
* Do not move diectories with many files to `/QRISdata`, tar or archive these first as lots of (small) files can cause problems (not just for you but also others).




