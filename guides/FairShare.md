# Bunya Fair Share 

Bunya employs fair share to ensure that every Bunya user can use an equal share of the computational resources.

### How does fair share work?

The total resources on Bunya are divided by the number of users on Bunya to determine the share of Bunya's resources for a single Bunya user. 

Every time a Bunya user runs a job on Bunya the job's use of resources is calculated after the job has finished. This usage is then charged in fair share to the user's account. This means each job (successfully completed, failed or cancelled) will reduce the user's fair share amount. A user's fair share amount can reduce down to zero.

The fair share amount of a Bunya user is used to calculate the priority (how high they sit in the queue) of the user's jobs. The lower the fair share amount the user has the lower the priority of the user's jobs. 

The fair share amount is constantly slowly refilling over time and the fair share will not remain zero for very long. This ensures that every user is able to keep running jobs.

* The jobs of a new user (or a user who has not run jobs in a while) will have very high priority and will most likely start very quickly.
* Once some jobs have finished the user's jobs will start to wait longer. This is normal and expected.
* This will not stop the user from submitting jobs and jobs will still start running once they have made their way up the queue.
* Priority of jobs in the queue are recalculated with every job finishing (of any user) and new jobs starting.
>[!IMPORTANT]
>* The fair share amount for each user is based on the total number of users registered in Bunya accounting groups. Bunya accounting group owners and administrators are advised to remove any user who has left their group promptly as this will increase the fair share amount of each user on Bunya.
>* Fair share is calculated per Bunya user. Being a member of more than one Bunya accounting group does not increase a user's fair share. Being in more than one Bunya accounting group is also a violation of RCC policy unless it has been discussed with and approved by RCC.

>[!CAUTION]
>* Each job is charged for **requested** resources. This means a job requesting 48 cores but is only using 10 is still charged for all 48 cores. And a job requesting a GPU is charged for the GPU no matter if it was used or not. This is because the requested resources are reserved for the job and cannot be used by other jobs. The only exception is walltime as resources are released when the job finishes.
>* A job leaving resources idle will still be charged.
>* **Inefficient use of resources is unfair to other users waiting in the queue and will impact the wait-time of future jobs.**

### Useful commands

You can use the command `squeue` to check why a job is sitting in the queue. In the command below the `%18p` will print out the priority of the job and `%S` will print out an estimated start time. The estimated start time will only be printed for jobs high enough in the queue to be considered by the scheduler. The jobs where this is *N/A* are still too low in the queue. `%16R` will print out the reason why a job is queueing. *Priority* means jobs with higher priority are in the queue before this job. *Resources* means the job is waiting for requested resources to become available. *QOSMax\*Limit* means that this job would bring the user over the maximum allowed resourcs per user.

`squeue --me -o "%12i %6q %.8P %.12j %.10u %.2t %.4D %.4C %.20b %10m %16R %18p %S"`

The command `sshare` can be used to check a user's fair share. 

`sshare -a | grep YourUsername`<br>
will print out the information below. The last value is the fair share. The value will be between `0` and `1`. With `1` being a full fair share and `0` being no fair share. 

```
Account                    User  RawShares  NormShares    RawUsage  EffectvUsage  FairShare 
-------------------- ---------- ---------- ----------- ----------- ------------- ----------
```

### User Limits

Bunya employs [per user limits](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#qos-use-and-limits) on total amount of resources that can be in use at any one time. When these limits are reached they will show a reason that is a `QOSMax*PerUserLimit`, or `JobArrayTaskLimit`, or `AssocGrpBillingMinutes` depending on the limit that has been reached.

For example, if a user has 4 GPUs in use, any further job will queue until the usage of the user drops below the limit of 4 GPUs. If the usage drops to 3 GPUs and the queued job needs 2 GPUs then this job will still stay queued as the usage needs to drop below of what the queued job requires to run. Once the usage is 2 GPUs the queued job can start as the current usage and new job now fit into the limit of 4 GPUs.


#### AssocGrpBillingMinutes

Most of the limits mkae it easy for users to see if their jobs have reached the limit or not. The limit on BillingMinutes is a bit different as it relates to the user's fair share usage which changes with time and the user's jobs finishing.<br>

User can obtain their BillingMinutes by using the command 

`sshare -a | grep YourUsername`<br>

The number given under RawUsage is BillingSeconds and BillingMinutes can be obtained by deviding RawUsage by 60.

Example
```

sshare -a | grep user1
 a_group1           user1          1    0.000472   720200160      0.014297   0.000392


720200160 / 60 = 12003336
```

user1 has over 12 million BillingMinutes in fair share usage. 

Once a user reaches 15 million BillingMinutes their jobs will no longer start and will show `AssocGrpBillingMinutes` as the reason. The user's `RawUsage` needs to drop below 15 million BillingMinutes, with enough margin to accommodate the user's next job, for the next job to start.

The RawUsage has a half-life of 28 days. This means the RawUsage decays (reduces) by 50% every 28 days, by 16% per 7 days, and by 2.4% per day.

Taking the half-life of the RawUsage into account, 15 million BillingMinutes are equivalent to a user running a job over 2 full Bunya CPU nodes or 2 H100 GPUs, 24/7 for 1 year. This amount of usage is similar to a small project grant on one of Australia's Tier 1 HPC facilites.



