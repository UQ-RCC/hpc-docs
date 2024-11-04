## Available partitions

The available partitions on Bunya are
```
general
gpu_rocm
gpu_cuda
gpu_sxm
```
## Available Quality of Service (QoS)

```
normal
debug
mig
sxm
gpu
```

## Available partitions and nodes

The available compute nodes on Bunya are listed in the table below. Please note while some feature the same CPU or GPU type, the available memory and/or number of CPUs or architecture can differ. Be mindful of this when requesting resources for jobs.

**Maximum walltimes**:<br>
general: 2 weeks (14 days, 336 hours)<br>
gpu_cuda, gpu_viz, gpu_rocm, gpu_sxm: 1 week (7 days, 168 hours)<br> 


| Partition | Hostnames |  Count |  CPU Memory (MB) | CPUS | FEATURES | GRES | Charge Multiplier|
|:---|:---|:---:|---:|:---:|:---|:---|---:|
| general | bun[006-008] | 3 | 4000000 | 192 | epyc3 | (null) | 1 |
| general | bun[009-067] | 59 | 2000000 | 192 | epyc3 | (null) | 1 |
| general| bun[083-115,126-143] | 51 | 1500000 | 192 | epyc4 | (null) | 1 |
|||||||||
| gpu_cuda | bun[003-004] | 2 | 2000000 | 256 | epyc3,<br> cuda,<br> cuda80gb | gpu:a100:3 | 50 |
| gpu_cuda | bun005 | 1 | 2000000 | 256 | epyc3,<br> cuda,<br> cuda10gb | gpu:nvidia_a100_80gb_pcie_1g.10gb:21 | 6 |
| gpu_cuda | bun068 | 1 | 2000000 | 192 | epyc3,<br> cuda,<br> cuda80gb | gpu:a100:2 | 50 |
|||||||||
| gpu_cuda | bun[071-076,116] | 7 | 2000000 | 192 | epyc3,<br> cuda,<br> cuda80gb | gpu:h100:3 | 100 |
| gpu_sxm | bun[117-120] | 4 | 1000000 | 192 | xeonsp4,<br> cuda,<br> cuda80gb,<br> sxm | gpu:h100:4 | 100 |
|||||||||
| gpu_cuda <br> gpu_viz | bun[077-082] | 6 | 2000000 | 192 | epyc3,<br> cuda,<br> cuda48gb | gpu:l40:3 | 40 |
| gpu_cuda <br> gpu_viz | bun[124-125] | 2 | 750000 | 192 | epyc4,<br> cuda,<br> cuda48gb | gpu:l40s:3 | 42 |
| gpu_viz | bun[121-123] | 3 | 750000 | 192 | epyc4,<br> cuda | gpu:a16:12 | 6 |
|||||||||
| gpu_rocm | bun[001-002] | 2 | 500000 | 192 | epyc3,<br> rocm | gpu:mi210:2 | 50 |
| gpu_rocm | bun070 | 1 | 380000 | 64 | epyc4,<br> rocm | gpu:mi210:2 | 50 |


## QoS use and limits

QoS are used to control access to resources and apply sustainable limits.<br> 

**Important:**<br>
mig requires the request of at least 1 MIG slice: gres=gpu:nvidia_a100_80gb_pcie_1g.10gb:1<br>
sxm requires the request of at least 1 H100:gres=gpu:h100:1<br>

| QOS |  Partitions |  Access| Priority | All User Group limit | User limits |
|:---|:---|:---:|:---:|:---|:---|
|||||||
| normal | general | open | 10 | 20000 CPUs, <br> 200 T CPU memory | 1536 CPUs,<br> 16 T CPU memory,<br> 0 GPUs,<br> 5000 jobs submitted | 
| debug | general, gpu_rocm, gpu_cuda, gpu_viz | open | 20 | none | 1 hour, <br> 1536 CPUs, <br> 16 T CPU memory, <br> 4 GPUs, <br> 2 jobs running, <br> 20 jobs submitted |
| gpu | gpu_rocm, gpu_cuda, gpu_viz | open | 10 | none | 256 CPUs, <br> 2 T of CPU memory, <br> 4 GPUs, <br> 4 jobs running, <br> 100 jobs submitted |
| mig | gpu_cuda | open | 10 | none | 441 CPUs, <br> 1932 GB CPU memory, <br> 21 GPUs, <br> 1000 jobs submitted |
| sxm | gpu_sxm | approved users | 10 | none | 192 CPUs, <br> 1 T CPU memory, <br> 4 GPUs, <br> 4 jobs running, <br> 50 jobs submitted |


### Partitions 

#### `general`
QoS: normal, debug<br>
Maximum walltime: 2 weeks (14 days, 336 hours)<br>
CPU only partition<br>
epyc3 and epyc4 architecture bun[006-009,010-067] and bun[83-115,126-143]<br>

#### `gpu_rocm`
QoS: gpu, debug<br>
Maximum walltime: 1 week (7 days, 168 hours)<br>
Maximum GPUs: See QoS<br>
GPU partition bun[001-002, 070]<br>
2 AMD Mi210 per node (bun[001-002, 070]), [type]=mi210<br>
>[!CAUTION]
>**1 AMD Mi210 is charged 50 \* 1 CPU core**<br>

#### `gpu_cuda`
QoS: gpu, debug, mig<br>
Maximum walltime: 1 week (7 days, 168 hours)<br>
Maximum GPUs: See QoS<br>
GPU partition bun[003-005, 068, 071-076, 077-082, 116-120, 124-125]<br>
3 NVIDIA H100 per node (bun[071-076, 116-120]), [type]=h100<br>
3 NVIDIA L40 per node (bun[077-082]), [type]=l40<br>
3 NVIDIA L40s per node (bun[124, 125]), [type]=l40s<br>
3 NVIDIA A100 per node (bun[003-004]), [type]=a100<br>
3 NVIDIA A100 per node and 7 MIG per A100 (bun005), [type]=nvidia_a100_80gb_pcie_1g.10gb<br>
2 NVIDIA A100 per node (bun068), [type]=a100<br>
L40: 32 bit CUDA, single precision<br>
L40s: 32 bit CUDA single precision and 16 bit and TF32 CUDA, half precision.<br>
H100: 16 bit and TF32 CUDA, half precision<br>
>[!CAUTION]
>**1 NVIDIA H100 is charged 100 \* 1 CPU core**<br>
>**1 NVIDIA L40 is charged 40 \* 1 CPU core**<br>
>**1 NVIDIA L40s is charged 42 \* 1 CPU core**<br>
>**1 NVIDIA A100 is charged 50 \* 1 CPU core**<br>
>**1 NVIDIA A100 MIG (10GB of GPU RAM) is charged 6 \* 1 CPU core**<br>

#### `gpu_viz`
QoS: debug, gpu<br>
Maximum walltime: 1 week (7 days, 168 hours)<br>
Maximum jobs per user: See QoS<br>
Maximum GPUs: see QoS<br>
GPU partition bun[077-082, 121-125]<br>
3 NVIDIA L40 per node (bun[077-082]), [type]=l40<br>
3 NVIDIA L40s per node (bun[124, 125]), [type]=l40s<br>
12 NVIDIA A16 per node (bun[121-123]), [type]=a16<br> 
L40: 32 bit CUDA, single precision<br>
L40s: 32 bit CUDA, single precision and 16 bit and TF32 CUDA, half precision<br>
A16: Visualisation only
onBunya job submissions are automatically queued here unless submitted via the ExpertDesktop.<br>
>[!CAUTION]
>**1 NVIDIA L40 is charged 40 \* 1 CPU core**<br>
>**1 NVIDIA L40s is charged 42 \* 1 CPU core**<br>
>**1 NVIDIA A16 is charged 6 \* 1 CPU core**<br>


#### `gpu_sxm`
QoS: sxm<br>
Maximum walltime: 1 week (7 days, 168 hours)<br>
Maximum GPUs: See QoS<br>
GPU partition bun[117-120]<br>
4 NVIDIA H100 SXM per node (bun[117-120]), [type]=h100<br>
H100: 16 bit and TF32 CUDA, half precision<br>
>[!CAUTION]
>**1 NVIDIA H100 is charged 100 \* 1 CPU core**<br>








