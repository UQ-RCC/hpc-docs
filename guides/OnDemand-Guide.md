# Open OnDemand User Guide

## What is Open OnDemand?

Open OnDemand is a web portal that provides access to the Bunya supercomputer, allowing users to submit and monitor jobs, manage files, and use a desktop environment to run graphical jobs using software such as Jupyter.

## Accessing OnDemand

Users cannot use OnDemand unless they already have Bunya access. To apply for access to Bunya, [click here.](https://rcc.uq.edu.au/high-performance-computing)

Access OnDemand [here](https://bunya-ondemand.rcc.uq.edu.au/), users will need to log in with AAF, and may receive an MFA prompt.

Please be patient as the OnDemand dashboard loads, it can take time after authenticating.

## Files

Users can manage all of their files from their home directory, scratch and any scratch projects they have access to.

Users can rename, download or delete directories; view, edit, rename, download or delete individual files by clicking the 3 dots to the right of the file or directory name.

## Jobs

Users can view details of active jobs (and recently completed jobs) under Active Jobs.

New jobs can be created with the Job Composer. We have provided some templates for common job types, these can be edited as required depending on the users individual needs. (add more details on how to do this once we add the templates).

Creating a new job with the Job Composer does not submit the job to the Bunya queue. To submit to the queue, highlight the job to be submitted and click the green submit button.

Jobs can also be stopped or deleted on this page.

## Clusters

Launch Bunya shell access in a new browser tab. Users will need to log in with account details as if they were accessing Bunya from the terminal, including MFA using DUO passcode or push.

## Interactive Apps

Access a CPU desktop environment or a GPU desktop environment.
 * Users should give their job a meaningful name, select target partition and resources they require as they would through the terminal on Bunya. The account string will autofill. For more information on resources available see the [Bunya user guide.](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md)
 * If users choose a CPU job, the GPU field will be ignored and the job will not target GPU nodes.
 * After clicking launch, the page will redirect to the My Interactive Sessions page, the job number and status will appear. The user may need to wait for the resources to be allocated, once allocated the job status will change to "Running".
 * Click on Launch Desktop to open a new browser tab containing a desktop environment, users have file system access to all files (Caja), a terminal emulator (MATE terminal), internet browser access (Firefox), and other accessories such as text editors.
 * Users can use the terminal emulator to load modules, edit files, run jobs, etc. as normal on Bunya.

## My Interactive Sessions
* View and access any currently running interactive sessions.
* Users may have multiple sessions running at once.
* Users can kill running sessions by clicking Delete next to the desired session.

## Notes
* Users are still queueing for jobs to be scheduled as normal on Bunya, access to a desktop environment will not be instant.
* The job wall time will commence immediately upon resource allocation, monitor the Interactive Sessions page, as users will not be notified when the job starts.
* Matlab jobs should be run on a CPU desktop environment. If GPU resources are required, request a GPU partition (gpu_viz partition recommended) and use uq_vglrun.
* If running on a GPU desktop, accelerated matlab MUST be run with the -nosoftwareopengl argument on GPU, and non-accelerated matlab MUST NOT.
