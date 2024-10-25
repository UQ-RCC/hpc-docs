## Available partitions

The available partitions on Bunya are
```
general
gpu_rocm
gpu_cuda
gpu_viz
gpu_sxm
```
## Available Quality of Service (QoS)

```
normal
debug
mig
sxm
gpu
viz
```

## Available nodes

The available compute nodes on Bunya are listed in the table below. Please note while some feature the same CPU or GPU type, the available memory and/or number of CPUs or architecture can differ. Be mindful of this when requesting resources for jobs.


| Hostnames |  Count |  CPU Memory (MB) | CPUS | FEATURES | GRES |
|:---|:---:|:---:|:---:|:---:|:---|
| bun[006-008] | 3 | 4000000 | 192 | epyc3 | (null) |
| bun[009-067] | 59 | 2000000 | 192 | epyc3 | (null) |
| bun[083-115,126-143] | 51 | 1500000 | 192 | epyc4 | (null) |
|||||||
| bun[003-004] | 2 | 2000000 | 256 | epyc3,cuda,cuda80gb | gpu:a100:3 |
| bun005 | 1 | 2000000 | 256 | epyc3,cuda,cuda10gb | gpu:nvidia_a100_80gb_pcie_1g.10gb:21 |
| bun068 | 1 | 2000000 | 192 | epyc3,cuda,cuda80gb | gpu:a100:2 |
|||||||
| bun[071-076,116] | 7 | 2000000 | 192 | epyc3,cuda,cuda80gb | gpu:h100:3 |
| bun[117-120] | 4 | 1000000 | 192 | xeonsp4,cuda,cuda80gb,sxm | gpu:h100:4(S:0-1) |
|||||||
| bun[077-082] | 6 | 2000000 | 192 | epyc3,cuda,cuda48gb | gpu:l40:3 |
| bun[124-125] | 2 | 750000 | 192 | epyc4,cuda,cuda48gb | gpu:l40s:3 |
| bun[121-123] | 3 | 750000 | 192 | epyc4,cuda | gpu:a16:12 |
|||||||
| bun[001-002] | 2 | 500000 | 192 | epyc3,rocm | gpu:mi210:2 |
| bun070 | 1 | 380000 | 64 | epyc4,rocm | gpu:mi210:2 |

### Partitions 

#### `general`
QoS: normal, debug, viz
Maximum walltime: 2 weeks (14 days, 336 hours)<br>
CPU only partition<br>
epyc3 and epyc4 architecture bun[006-009,010-067] and bun[83-115,126-143]<br>

#### `gpu_rocm`
QoS: gpu, debug
Maximum walltime: 1 week (7 days, 168 hours)<br>
Maximum GPUs: See QoS<br>
GPU partition bun[001-002, 070]<br>
2 AMD Mi210 per node (bun[001-002, 070]), [type]=mi210<br>
>[!CAUTION]
>**1 AMD Mi210 is charged 50 \* 1 CPU core**<br>

#### `gpu_cuda`
QoS: gpu, debug, viz, mig
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
QoS: debug, gpu, viz
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
QoS: sxm
Maximum walltime: 1 week (7 days, 168 hours)<br>
Maximum GPUs: See QoS<br>
GPU partition bun[117-120]<br>
4 NVIDIA H100 SXM per node (bun[117-120]), [type]=h100<br>
H100: 16 bit and TF32 CUDA, half precision<br>
>[!CAUTION]
>**1 NVIDIA H100 is charged 100 \* 1 CPU core**<br>

### QoS use and limits

QoS are used to control access to resources and apply sustainable limits. 

#### normal
Partitions: general<br>
Access: all users<br>
Priority: 10<br>
Group (all users) limits: 21000 CPUs, 210 T CPU memory<br>
User limits: 1536 CPUs, 16 T CPU memory, 0 GPUs, 5000 jobs submitted <br>
Minimum requested resources: none<br>

#### debug
Partitions: general, gpu_rocm, gpu_cuda, gpu_viz <br>
Access: all users<br>
Priority: 20<br>
Group (all users) limits: none<br>
User limits: 1 hour, 1536 CPUs, 16 T CPU memory, 4 GPUs, 2 jobs running, 20 jobs submitted <br>
Minimum requested resources: none<br>

#### gpu
Partitions: gpu_rocm, gpu_cuda, gpu_viz <br>
Access: all users<br>
Priority: 10<br>
Group (all users) limits: none<br>
User limits: 256 CPUs, 2 T of CPU memory, 4 GPUs, 4 jobs running, 100 jobs submitted <br>
Minimum requested resources: none<br>

#### mig
Partitions: gpu_cuda<br>
Access: all users<br>
Priority: 10<br>
Group (all users) limits: none <br>
User limits: 441 CPUs, 1932 GB CPU memory, 21 GPUs, 1000 jobs submitted <br> 
Minimum requested resources: gres=gpu:nvidia_a100_80gb_pcie_1g.10gb=1<br>

#### viz
Partitions: general, gpu_cuda, gpu_viz <br>
Access: all users<br>
Priority: 20<br>
Group (all users) limits: none<br>
User limits: 24 hours, 192 CPUs, 4 GPUs, 2 jobs running, 20 jobs submitted <br>
Other limits: 1 node only
Minimum requested resources: none<br>

#### sxm
Partitions: gpu_sxm<br>
Access: After approved application<br>
Priority: 10<br>
Group (all users) limits: none <br>
User limits: 192 CPUs, 1 T CPU memory, 4 GPUs, 4 jobs running, 50 jobs submitted  <br> 
Minimum requested resources: gres=gpu:h100=1<br>





