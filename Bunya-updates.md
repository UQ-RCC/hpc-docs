# Latest Updates and Changes to the Bunya HPC Cluster

## 27 January 2026

* The next scheduled maintenance on Bunya will occur between 9pm Monday 9th March and 9pm Tuesday 10th March.
* There will be no access to Bunya during the maintenance. This includes no access to data in /home, /scratch/user and /scratch/project.
* Bunya queues will not schedule jobs that would run into the maintenance window.

## 9 December 2025

* The RCC will be performing an operating system upgrade on Bunya in early 2026.
* All software modules that rely on gcc-10, foss-2021a, intel-2021a, or gompi-2021a will be deprecated as they are not supported on the new OS.
* A list of modules that will be deprecated has been published [here](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/2021a-software-modules.md).
* User compiled modules that depend on any of the deprecated modules will stop working after the upgrade, so recompiling against the latest available versions of module dependencies is strongly recommended.
* All gcc-11, and 2022a modules will also be deprecated by the end of 2026, so using the latest available versions will lead to the least disruptions to productivity.
* Users who are currently using modules on the list to be deprecated, that don't have a newer version available, should email rcc-support@uq.edu.au as soon as possible.

## 12 November 2025

* 90 day file expiry on /scratch has now commenced. Any files that have not been accessed in 90 days will be deleted automatically on a daily basis.
* A reminder that /scratch/user, /scratch/project, and /home are not backed up, and once deleted files in these location cannot be recovered.

## 10 October 2025

* To improve the availability of GPU resources on Bunya and prevent users from unintentionally reducing their fair share, the RCC will start automatically delete jobs that leave GPU resources idle.
* Start date: Monday 27 October 2025.
* The RCC will review the impact on queues and GPU resource wait times and if required consider stricter time frames. In future, the automatic deletion of jobs that leave resources idle will be extended to CPU only jobs.

## 3 October 2025

* UQRDM Q collections will not be accessible from Bunya or onBunya tomorrow, due to scheduled maintenance.
* Maintenance window: 8am to 8pm Saturday 4 October 2025.
* During this time users will not be able to access their Q storage record in /QRISdata. Users should not submit any jobs that rely on access to /QRISdata during this time. They should also consider putting queued jobs that rely on access to /QRISData on hold until after the maintenance. Jobs that rely on access to /QRISdata and are running into the maintenance window might crash.

## 11 September 2025

* The scheduled November quarterly maintenance has been postponed to align with the arrival of new hardware being added to Bunya. The new maintenance date will be announced at least 2 weeks in advance.
* The daily automatic deletion of files in /scratch/user and /scratch/project that was scheduled to commence at November quarterly maintenance will still start as scheduled. Any files that have not been accessed in 90 days will be deleted automatically starting on Wednesday 12 November 2025.

## 8 September 2025

* Processes from VScode, Cursor, PyCharm/JetBrains and other IDE's on the login nodes will now be killed via an automated process. This may be extended to other processes in the future.
* In many cases this will terminate user processes running on compute nodes. To avoid this, users should not use the IDE to connect to Bunya and users should not attach the IDE to an interactive job. Users should start a job first and then start the IDE on the actual compute node inside a job.
* A VScode app is now available via onBunya that users are encouraged to use.
* Users are reminded that no processes should be run on the login nodes. This includes R and Python, conda, python, pip, and R software environment installation, make and other compile processes, and servers.

## 20 August 2025

* To ensure that adequate scratch space is available for computation, the RCC is working on implementing automatic deletion of files that have not been accessed in over 90 days from /scratch/user and /scratch/project. This is planned to start after the November quarterly maintenance.

## 4 August 2025

* The next scheduled maintenance on Bunya will occur between 9pm Monday 11th August and 9pm Tuesday 12th August.
* There will be no access to Bunya during the maintenance. This includes no access to data in /home, /scratch/user and /scratch/project.
* Bunya queues will not schedule jobs that would run into the maintenance window.

## 20 May 2025

* Multiple versions of PMIx are now available on Bunya. As a consequence, users that run MPI codes built with foss/2021a, need to provide the following additional option to their srun command to ensure the correct version of PMIx is used: 

  `srun  --mpi=pmix_v4  <your_usual_srun_command>`

## 16 May 2025

* Version 6.4.0 of the ROCm software stack is now available on Bunya AMD GPU nodes, and has been set as the default rocm module. ROCm 6.0.1 is no longer available.

## 14 April 2025

* The next scheduled maintenance on Bunya will occur between 9pm Monday 12th May and 9pm Tuesday 13th May.
* There will be no access to Bunya during the maintenance. This includes no access to data in /home, /scratch/user and /scratch/project.
* Bunya queues will not schedule jobs that would run into the maintenance window.

## 6 January 2025

* The next scheduled maintenance on Bunya will occur between 9pm Monday 10th February and 9pm Tuesday 11th February.
* There will be no access to Bunya during the maintenance. This includes no access to data in /home, /scratch/user and /scratch/project.
* Bunya queues will not schedule jobs that would run into the maintenance window.
* Please note there has been a change to the quarterly maintenance schedule, and maintenance will now be performed on the second Tuesday of February, May, August and November. In the past it has been performed on the first Tuesday of these months.

## 5 November 2024

* Bunya partitions and how to request GPUs and debug priority has changed.
* Available partitions are:
  * general (this is the default partition)
  * gpu_cuda
  * gpu_rocm
  * gpu_viz (onBunya specific and should not be used outside of onBunya)
  * gpu_sxm (approved users only)

* There is a 2-week limit on walltime for general and a 1-week limit on all GPU partitions.
* There are no higher priority partitions. Higher priority, such as for debug jobs, is now done by requesting a QoS (quality of service) with --qos=name.
* Available QoS:
  * normal (this is the default and allows no GPU)
  * gpu
  * debug (higher priority but limits resources)
  * mig
  * sxm

## 21 October 2024

* The next scheduled maintenance on Bunya will occur between 9pm Monday 4th November and 9pm Tuesday 5th November.
* There will be no access to Bunya during the maintenance. This includes no access to data in /home, /scratch/user and /scratch/project.
* Bunya queues will not schedule jobs that would run into the maintenance window.
* Wiener is not affected by this maintenance and will remain open to users. Wiener will be shutdown and decommissioned on Friday 29th of November 2024.

## 13 August 2024

* The way users use DUO for multifactor authentication has changed. After you enter your password, you will now need to enter a 6 digit passcode from the DUO app, this replaces push notification approval.
* QCIF users (non UQ) can now use their QSAC password [https://services.qriscloud.org.au/credential](https://services.qriscloud.org.au/credential) to access Bunya and ssh keys are no longer required.
* A new tool, jobstats, is now available as a module to Bunya users to monitor the resource utilization of their jobs. The following commands will show visual and numerical CPU, CPU ram, GPU, and GPU ram utilization:

  ```
  module load jobstats
  
  jobstats <JobID>
  ```

## 30 July 2024

* The next scheduled maintenance on Bunya will occur between 7pm Monday 5th August and 9pm Tuesday 6th August.
* There will be no access to Bunya during the maintenance. This includes no access to data in /home, /scratch/user and /scratch/project.
* Bunya queues will not schedule jobs that would run into the maintenance window.

## 21 June 2024

* RDM in /QRISdata will not be accessible between Monday, 24 June 2024, 5:00pm and Tuesday, 25 June 2024, 12:00am due to a planned outage.

## 23 April 2024

* The next scheduled maintenance on Bunya will occur between 9pm Monday 6th May and 9pm Tuesday 7th May.
* There will be no access to Bunya during the maintenance. This includes no access to data in /home, /scratch/user and /scratch/project.
* Bunya queues will not schedule jobs that would run into the maintenance window.

## 22 February 2024

* Issues with Jupyter in [Open OnDemand](https://bunya-ondemand.rcc.uq.edu.au) have been resolved.
* MIG has been enabled for some A100 GPUs. This allows you to request a lower-powered GPU and get a cheaper FairShare charge. Please see the [user guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md) for details.

## 29 January 2024

* The next scheduled maintenance on Bunya will occur between 9pm Monday 5th February and 9pm Tuesday 6th February.
* There will be no access to Bunya during the maintenance. This includes no access to data in /home, /scratch/user and /scratch/project.
* Bunya queues will not schedule jobs that would run into the maintenance window.

## 1 December 2023

* RCC Support will be unavailable over the Christmas break from the 23rd of December 2023 to the 1st of January 2024 inclusive, and will reopen on the 2nd of January 2024.
* The last Hacky Hour for the year will be on the 5th of December 2023. Hacky Hour will resume on Tuesdays as usual on the 30th January 2024.
* The last Virtual HPC user support meetup for the year will be on the 14th of December 2023. vHPC will resume on Thursdays as usual on the 11th January 2024.

## 17 October 2023

* The next scheduled maintenance on Bunya will occur between 9pm Monday 6th November and 9pm Tuesday 7th November.
* There will be no access to Bunya during the maintenance. This includes no access to data in /home, /scratch/user and /scratch/project.
* Bunya queues will not schedule jobs that would run into the maintenance window.

## 15 September 2023

* The beta partitions should no longer be targeted as all of the Bunya phase 2 nodes have now been moved into the general and debug queues.
* Users who compile their own software will now need to target specific architecture (epyc3 or epyc4) to be able to compile and run jobs as expected. Refer to the [user guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md) for more information.

## 29 August 2023

* H100 and L40 GPU's are now available for use on partition "gpu\_cuda".
* L40 GPU's are now available for use on partition "gpu\_viz".

## 24 August 2023

* Bunya phase 2 introduces 33 new AMD Genoa epyc4 nodes for use on partition "general\_beta".
* As there is now a mix of epyc3 and epyc4 nodes, the correct architecture must be targeted, see [hpc-docs/Bunya-User-Guide.md](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md) for more details on how to do this. 
