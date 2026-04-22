# CryoSPARC User Guide

## Introduction
[CryoSPARC](https://cryosparc.com) is a suite of tools for cryo-EM research workflows. It is available on Bunya, though due to its design there are certain considerations to make when using it and some features involving multi-user collaboration are unusable.

## Installing CryoSPARC
You will run your own CryoSPARC instance, therefore you will need to obtain a license key. The license is free for non-profit academic use. The key is in UUID format. It looks like this: `01234567-89ab-cdef-0123-456789abcdef`. You will need this key to install the software.

In the onBunya menu, there are two CryoSPARC entries, "CryoSPARC" and "CryoSPARC updater (to <version>)". Select "CryoSPARC" to install or use the software. The updater will only update existing installations to the latest version on Bunya. You are free to change the version you use via command line tools. The CryoSPARC website has extensive documentation on how to use the command line tools.

When you launch CryoSPARC for the first time, it will detect that you do not have the software installed yet, and begin the installation process. You will see a terminal window with brief instructions for entering the information the software needs to install. Enter your license key when asked.

You will be asked to create a user account, with an email address, first and last names, username and password. This will be used to log in to CryoSPARC's web interface, and it can be anything. They do not need to be a real email address or your real name, and the default options provided are fine and the default password is randomly generated. These credentials are stored in plain text in your home directory, in the file `/home/yourusername/cryosparc-default-user.txt`. Therefore, **do not use your Bunya login credentials!**

## Running CryoSPARC
The same "CryoSPARC" menu item in onBunya that you used to install CryoSPARC will also launch it. A terminal window will open, with a log of events that occur during the startup process. When it is finished, it will open Firefox to the web interface. Log in with the email address and password you set during installation. Do not close the terminal window. To exit CryoSPARC, close Firefox and allow the terminal to perform shutdown tasks and close itself.

CryoSPARC jobs are sent to "lanes" for processing. There are two types of lane, one that runs in the desktop job with the master, called "default", and several cluster lanes. The lanes are created every time you launch CryoSPARC, so that the default lane updates with the number of CPUs and GPUs available to it from your desktop session. The cluster lanes give you access to different kinds of GPU as well as options for shorter and longer running jobs. You do not need to use a GPU desktop to run CryoSPARC, though if you do have a GPU desktop, you can run CryoSPARC jobs that require a GPU in the default lane.

CryoSPARC may give errors if the desktop does not have enough compute resources. It works best with at least a Medium desktop (8 cores, 64GB of RAM).

CryoSPARC must be running while jobs in the cluster lanes are running. This can cause problems when you queue a job to a cluster lane that does not start for several hours and you run the risk of your onBunya desktop running out of time before the CryoSPARC job can run. You can reduce the chances of this by running CryoSPARC in an Expert Desktop, where you can schedule for longer than 24 hours. If you are going to use an Expert Destop with a GPU, please ensure you make efficient use of the GPU and run jobs as much as possible during the time you have the desktop.

If your desktop job runs out of time, it will be stopped and this can cause corruption to your CryoSPARC database. Please ensure you stop CryoSPARC manually by closing your Firefox window and letting the terminal program complete its shutdown tasks.

## Troubleshooting
There are a variety of common errors you might see when running CryoSPARC. If you cannot fix the error yourself, open a ticket with RCC support for help. The first thing to check is that your home directory's file usage is below quota. Run the `rquota` command in a terminal, or select `Files -> GPFS Quota` in onBunya (the website, not in a desktop session) to check this, and if you are over quota you will have to move or delete files to return under quota.

CryoSPARC can use a very large amount of storage, and it is quite common to run out of quota after extended use. You should detach and store projects in an RDM collection when you are not using them to save space in your scratch and home directories. Also note that files in scratch directories that have not been accessed in 90 days will be deleted automatically. This can cause significant data loss to your project beyond just the files that were deleted and you should at least make a backup copy of your project and older jobs that you do not need to rerun within this 90 day period. You can do this in stages, e.g. after image import, after motion correction and CTF estimation, and after model training. Look into using the `rsync` command line utility to copy changes from your project directory to the archival copy in your collection.

### Web interface does not connect to CryoSPARC
There is probably an error message in the terminal window. The most likely cause is a failure to start the database service. You can use a command line utility to check the database for errors: `cryosparcm database check`. If you get a "command not found" error, your cryosparcm command is not in your path and you will have to run `~/cryosparc/cryosparc_master/bin/cryosparcm database check` instead.

### Job fails with "no heartbeat received" error
The job you scheduled started, but crashed. In your project directory will be a job directory named after the job number like 'Jnn'. There will be files in there that log the output of the job as it ran. Look there for more details on the error that crashed the job.

### Project won't attach
If you have detached a project, either for storage or to share with another user, you may have to go to the project directory and manually delete any `cs.lock` files you find before you can re-attach it.

### My login doesn't work anymore
This is often a sign of deeper database corruption, but you can restore the user account you had by running this command, using the account you created when you installed CryoSPARC. The details are saved in your home directory in the file `cryosparc-default-user.txt`

cryosparcm user create --email "<email@address>" --firstname "<first name>" --lastname "<last name>" --username "<username>" --password "<password>" --role "admin"

And check your database using the `cryosparcm database check` command as described above. You may have to delete your entire database and re-create it, then re-attach your projects. To do so, you can make a backup of your ~/cryosparc/cryosparc_database directory by copying it e.g. to your scratch directory. Then delete that directory and all its contents, then restart CryoSPARC. You will have to create a user account as described above, then re-attach your projects (you may need to delete cs.lock files as described above).