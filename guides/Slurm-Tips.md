# Slurm Tips for subnitting to GPU nodes on Bunya

A collection of practical Slurm submission tips for getting the most out of Bunya's scheduling and GPU resources. 

When queue times seem longer than expected, first check whether your resource request is more restrictive than your application actually requires. Broadening GPU selection (for example, allowing both gpu_cuda and gpu_sxm H100 resources) and using appropriate QoS settings can significantly improve job start times while still meeting application requirements.

## Target 40GB MIG GPU Slices

For workloads that fit within a 40GB MIG slice on either A100 or H100 hardware:

```
#SBATCH --gres=gpu:1
#SBATCH --partition=gpu_cuda
#SBATCH --constraint=cuda40gb
#SBATCH --batch=cuda40gb
```


This will target the 40GB CUDA-capable MIG resources regardless of whether they are hosted on A100 or H100 GPU nodes.

## Target 80GB GPUs

For workloads that require a full 80GB GPU:

```
#SBATCH --gres=gpu:1
#SBATCH --partition=gpu_cuda
#SBATCH --constraint=cuda80gb
#SBATCH --batch=cuda80gb
```

This allows Slurm to schedule the job onto suitable 80GB A100 or H100 resources.

## Target any H100

The H100 nodes in the `gpu_cuda` and the `gpu_sxm` partition are a different architecture. If your code can run on both standard H100 and H100 SXM nodes, you can allow Slurm to schedule on either partition:

```
#SBATCH --gres=gpu:h100:1
#SBATCH --partition=gpu_cuda,gpu_sxm
```

This generally improves scheduling flexibility and can reduce queue times.

### Detecting SXM vs non-SXM at runtime

In job scripts, you can use the partition assigned to the job to determine whether you landed on an SXM system:

```
if [ "$SLURM_JOB_PARTITION" = "gpu_sxm" ]; then
   echo "Running on H100 SXM"
   # Use SXM-specific code path
elif [ "$SLURM_JOB_PARTITION" = "gpu_cuda" ]; then
   echo "Running on standard H100"
   # Use standard code path
fi
```

This is useful when maintaining separate application builds or tuning parameters for different H100 platforms.

## Target 40GB and 48GB GPUs

For jobs that can run on a GPU with 40GB or 48GB you can target either of these with the **`Or`** option for the node features.

```
#SBATCH --partition=gpu_cuda
#SBATCH --constraint="[cuda40gb|cuda48gb]"
#SBATCH --batch="[cuda40gb|cuda48gb]"
```

This allows the job to be scheduled to the 40GB MIG slices (A100 or H100) or the L40s GPUs.

## Use the right QoS for short jobs to reduce wait time

### debug QoS

- Software installation
- Environment testing
- Pipeline validation
- Interactive debugging
- Short development runs

Use:

```
#SBATCH --qos=debug
#SBATCH --time=1:00:00
```

Characteristics:

- Maximum walltime: 1 hour
- Up to 2 concurrent running jobs
- 20 jobs submitted
- Priority: 30

Compared with the `general` (CPU only) and `gpu` QoS priority of 10, `debug` jobs are scheduled with higher priority.

### short QoS

For jobs that need more time but are still relatively short-lived:

```
#SBATCH --qos=short
#SBATCH --time=12:00:00
```
Characteristics:

- Maximum walltime: 12 hours
- Up to 2 concurrent running jobs
- 20 jobs submitted
- Priority: 20

Use the most specific constraint that matches your requirements. Specifying a compatible GPU family or memory size instead of targeting one specific GPU type only can often improve queue times.

## gpu_viz partition restrictions

The gpu_viz partition is reserved exclusively for onBunya desktop sessions. Do not submit jobs to this partition using `sbatch` or `salloc`


