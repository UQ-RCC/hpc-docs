# Basics of Connecting to RDM Q Storage Allocations

Please also refer to 
- the [Bunya Storage User Guide section](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-UserData-Guide.md#qrisdata) and
- the [RCC's RDM Guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/RDM-guide.md) as well as
- the [UQ RDM portal](https://rdm.uq.edu.au)


## Document Purpose
This document's focus is the key concepts for using RDM Q as they relate to integrating RDM within your computational workflows.

## Accessing RDM from PC

|Gateway|Who it is for|How|Local Aliases|Notes|
|:---|:---:|:---|:---|:---|
|St Lucia Gateway|Everybody|\\\\uq.edu.au\UQ-Research|R: Drive|Windows|
|||\\\\shares01.rdm.uq.edu.au|RDM Share|Windows|
|||smb://shares01.rdm.uq.edu.au|RDM Share|MacOS and Linux|
|Institutes Gateway #1|AIBN|\\\\uq.edu.au\UQ-Inst-Gateway1|data.aibn.uq.edu.au|Q storage allocations only.</br>You need to request that it be mounted.|
||CAI|\\\\uq.edu.au\UQ-Inst-Gateway1|data.cai.uq.edu.au|Q storage allocations only.</br>You need to request that it be mounted.|
||QBI|\\\\uq.edu.au\UQ-Inst-Gateway1|data.qbi.uq.edu.au|Q storage allocations only.</br>You need to request that it be mounted.|
||IMB|\\\\uq.edu.au\UQ-Inst-Gateway1|data.imb.uq.edu.au|Q storage allocations only.</br>You need to request that it be mounted.|
|<del>Institute Gateway #2</del>||||The Institute Gateway #2 hardware has been decommissioned.</br>|

Note:<br>
<br> 
All Institute users now access their RDM Q storage allocations via the Institute Gateway #1.

## Requesting your RDM Q storage allocation be mounted on an Institutes Gateway

The _owner_ of RDM Q storage allocations should email *rcc-support@uq.edu.au* to request that it be mounted. </br>
Please provide details of the collection and confirm that you are the owner.</br>

## Accessing RDM from Bunya HPC

All Q storage allocations can be accessed from Bunya HPC. The filepath will look like `/QRISdata/Q1234` 

It is *not* possible to mount A or I type RDM collection storage allocations onto the HPC.

Users of onBunya service are provided with convenient short cuts on the desktop to access the RDM Q storage allocations that they are the owner of, or collaborator with.

Please refer to the [Bunya Storage User Guide section](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-UserData-Guide.md#qrisdata) on using RDM Q collections on Bunya and the [RDM Guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/RDM-guide.md) for more details.


## Document Updated

August 21 2026
