**DRAFT** 20250904

# Basics of RDM Q Storage Allocations

## Document Purpose
This document's focus is the key concepts for using RDM Q as they relate to integrating RDM within your computational workflows.

## Accessing RDM from PC

|Gateway|Who it is for|How|Local Aliases|Notes|
|:---|:---:|:---|:---|:---|
|St Lucia Gateway|Everybody|\\\\uq.edu.au\UQ-Research|R: Drive|Windows|
|||\\\\shares01.rdm.uq.edu.au||Windows|
|||smb://shares01.rdm.uq.edu.au||MacOS and Linux|
|Institute Gateway #1|AIBN|\\\\uq.edu.au\UQ-Inst-Gateway1|data.aibn.uq.edu.au|Q storage allocations only|
||CAI|\\\\uq.edu.au\UQ-Inst-Gateway1|data.cai.uq.edu.au|Q storage allocations only|
||QBI|\\\\uq.edu.au\UQ-Inst-Gateway1|data.qbi.uq.edu.au|Q storage allocations only|
|Institute Gateway #2|IMB|\\\\uq.edu.au\UQ-Inst-Gateway2|data.imb.uq.edu.au|Q storage allocations only|

## Accessing RDM from Bunya HPC

All Q storage allocations can be accessed from Bunya HPC. The filepath will look like `/QRISdata/Q1234` 

It is *not* possible to mount A or I type RDM collection storage allocations onto the HPC.

Users of onBunya service are provided with convenient short cuts on the desktop to access the RDM Q storage allocations that they are the owner of, or collaborator with.

Please refer to the [Bunya Storage User Guide section](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-UserData-Guide.md#qrisdata) on using RDM Q collections on Bunya.

## Computational Workflows that incorporate RDM

### A common workflow example

### Job dependencies are your friend

### Pre-staging data using appropriate resources

### Use the special tools for the special work

### Post-processing considerations

## Best Practices for using RDM with Bunya HPC



