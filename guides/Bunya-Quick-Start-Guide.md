# UQ Bunya HPC Quick Start Guide

## 1. Access Bunya

Before using Bunya you must have:

- [An approved Bunya account](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#applying-for-access).
- Multi-factor authentication configured.
- Be a member of a Bunya Slurm accounting group.

Connect using SSH:

```
ssh username@bunya.rcc.uq.edu.au
```

Alternatively, use **onBunya** ([the web-based portal)](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/OnDemand-Guide.md) for interactive applications such as Jupyter, RStudio and VS Code. 

Important:

- VS Code and other IDEs are not permitted on Bunya login nodes
- Remote tunnelling to Bunya is not permitted

[More information](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#connecting).

---

## 2. Understand the filesystems

Bunya provides several storage locations:

| Location | Purpose |
|----------|---------|
| `/home` | Configuration files, software, scripts |
| `/scratch/user` | Temporary working data |
| `/scratch/project` | Shared group workspaces |
| `/QRISdata` | RDM-Q and legacy storage allocations (long-term research data storage) |
| `/scratch/opendata` | Shared open data sets and models |
| `/scratch/licenseddata` | Shared licensed data sets |

Important:

- Scratch storage is temporary.
- Files in `/scratch/user` and `/scratch/project` that have not been accessed for 90 days may be automatically deleted.
- Users should move important data to an appropriate long-term storage solution.

For more information, including quotas on `/home` and `/scratch`, and appropriate usage of `/QRISdata` see the [Bunya data user guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-UserData-Guide.md) and the [RDM user guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/RDM-guide.md).

---

## 3. Load Software Modules

Bunya uses software modules, see [here](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#software) for more information.

Find available software, use keywords:

```
module avail
module avail miniforge
```

Load software, name and version required:

```
module load miniforge/26.1.0-0
```

Check loaded modules:

```
module list
```

Many common research applications, compilers, MPI libraries and scientific software packages are available through modules. For a compact list of Bunya software modules and onBunya applications see [here](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/List-of-Software.md).
 
---

## 4. Test an interactive job

Bunya uses the **Slurm** workload manager for scheduling jobs. 

Do not run computational workloads on the login nodes. Interactive work, including software installations, software compilations, quick tests, should be performed inside an allocated job. 

[Example interactive session](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#interactive-jobs-1):

```
salloc --nodes=1 --ntasks-per-node=1 --cpus-per-task=1 --mem=5G --job-name=CHANGE-ME --time=01:00:00 --partition=general --qos=debug --account=AccountString srun --export=PATH,TERM,HOME,LANG --pty /bin/bash -l
```
- Change *AccountString* to your assigned [AccountString](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#what-is-my-accountstring-)

---

## 5. Submit your first batch job

For information on all the different options for Slurm scripts see [here](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#slurm-scripts)

Create a script called `hello.slurm`:

```
#!/bin/bash --login
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=10G
#SBATCH --job-name=hello
#SBATCH --time=1:00:00
#SBATCH --qos=debug
#SBATCH --partition=general
#SBATCH --account=AccountString  ##FIX THIS
#SBATCH -o slurm-%j.output
#SBATCH -e slurm-%j.error

# module loads go before starting your program
# use srun before the executable 

echo "Hello from Bunya"
hostname
date
```
- Change *AccountString* to your assigned [AccountString](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#what-is-my-accountstring-)

Submit the job:

```
sbatch hello.slurm
```

Monitor it:

```
squeue 
```
The output will be in `slurm-JobID.output`.

See example scripts for [CPU single node](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#simple-script-for-cpus-and-single-node), [CPU MPI](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#simple-mpi-script-using-192-cores-as-an-example-using---ntasks-will-spread-the-job-over-multiple-nodes-where-there-is-space), [job array](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#job-arrays).

Please check available [partitions](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#available-partitions-and-nodes) and associated hardware and available [QoS](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#qos-use-and-limits) and their limits.
 
---

## 6. Running GPU Jobs

Available GPU partitions include:

- `gpu_cuda`
- `gpu_rocm`
- `gpu_sxm` 
- `gpu_viz` (only for onBunya use) 

Example GPU request:

```
#SBATCH --partition=gpu_cuda
#SBATCH --gres=gpu:h100
#SBATCH --qos=gpu
```
Only request GPUs you can actively use. Jobs that leave GPUs idle are automatically terminated.

See example scripts for [Cuda GPUs](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#simple-script-for-cuda-gpus) and [ROCM GPUs](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#simple-script-for-amd-rocm-gpus).

---

## 7. Monitor Resource Usage

A useful monitoring tool is:

```
module load jobstats/2024.08
jobstats <jobid>
```
This displays max CPU, max CPU and GPU memory, and average GPU utilization for running and completed jobs. It also provides a link to a graphical dashboard showing the jobs history.

---

## 8. Using Conda (Optional)

For Python workflows:

```
module load miniforge/2026.1.0-0
source $ROOTMINIFORGE/etc/profile.d/conda.sh

conda create -n myenv python=3.11
conda activate myenv
```
For guidance on managing Conda environments on Bunya see the [Conda guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/conda-environment.md).

---

## 9. Good Practices

✅ Run computations through Slurm jobs  
✅ Keep large datasets in shared spaces provided  
✅ Use scratch space for active computation  
✅ Monitor utilization and optimize resource requests  
✅ Use onBunya for interactive tools and IDEs  

❌ Do not run Python, R, compilations, or IDEs or filesystem intensive tasks (e.g. copy, rsync, tar, zip/unzip) directly on login nodes 

---

