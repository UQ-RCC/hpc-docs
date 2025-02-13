# Latest Updates and Changes to the Bunya HPC Cluster

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

  module load jobstats 

  jobstats JobID

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
