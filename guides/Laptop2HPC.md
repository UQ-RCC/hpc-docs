### Using R on Bunya - Making the move from Laptop to HPC

_This document was the basis of a presentation to The University of Queensland R Users Group meetup on April 24 2024 by Dr David Green UQ RCC_

<!-- https://bootswatch.com/ -->
<!-- bootswatch:  default _minty_  celurean solar cyborg  quartz  zephyr   -->

## Abstract

In this session, we will trace the steps taken by the many UQ
researchers using R who have wanted, or needed, stronger (or more
numerous) computers on which to run their codes.

There are tremendous benefits to porting your R computations to the
high-performance computing (HPC) environment.

But there are also some obstacles to overcome, especially with the ease
of use and there are a few gotchas.

Some recent innovations on the Bunya HPC system are addressing some of
those obstacles.

## Outline

-   So you’ve got some R code running on your laptop and you’ve hit
    limits?
-   HPC 101
-   Implications for your code
-   R on Bunya
-   Access Modes
-   Parameter Sweeps

### Your R code

Imagine the scenario where your R code

-   Is showing promise,
-   Needs to be run more extensively,
-   Is already hitting limits when running on your laptop.

### Laptop limitations

-   Code could run faster with more cores,
-   Insufficient RAM,
-   Disk space is small,
-   The laptop is unusable for other work,
-   Smoke comes out when it’s running your code ;-)

### Enter Bunya, for comparison

|                       |     This Laptop     |     Bunya Phase 1     |     Bunya Phase 2     | Bunya Phase 3 soon |
|:----------------------|:-------------------:|:---------------------:|:---------------------:|--------------------|
| CPU                   | Intel Core i7-8650U | AMD EPYC 7643 (Milan) | AMD EPYC 9454 (Genoa) |                    |
| Speed                 |      2.11 GHz       |       2.30 GHz        |       2.75 GHz        |                    |
| Sockets               |          1          |           2           |           2           |                    |
| Cores                 |          4          |          96           |          96           |                    |
| Logical Processors    |          8          |          192          |          192          |                    |
| RAM                   |        16 GB        |        2.0 TB         |        1.5 TB         |                    |
| Number of Devices     |     1 (usually)     |          62           |          33           |                    |
| Total number of cores |          4          |         5952          |         3168          |                    |

#### And that’s not all of Bunya !!

-   Some Bunya nodes have 4TB.
-   Several other Phase 2 nodes have state-of-art GPU computing
    capabilities.
-   R has limited support for GPU
-   See
    [gpuMatrix](https://cran.r-project.org/web/packages/GPUmatrix/index.html)
    package, for example.

### HPC 101

-   HPCs are built for speed, not for comfort !
-   HPCs are almost always a command line linux platform.
-   HPCs are almost always batch mode environments.
-   Job scripts are created and submitted to the batch system.
-   Jobs need to be able to run “with the lights out”.
-   Jobs need to be able to run without user intervention.
-   Many HPCs (including Bunya) support interactive use via the batch
    system.
-   Some HPCs (including Bunya) have graphical capabilities for user
    access.
-   Some HPCs (not Bunya) are based on the Windows operating system.

#### Structure of Bunya HPC

<figure>
<img
src="https://github.com/UQ-RCC/hpc-docs/blob/main/media/HPC_Cluster_Schematic.png?raw=true"
alt="Schematic of a HPC Cluster" />
<figcaption aria-hidden="true">Schematic of a HPC Cluster</figcaption>
</figure>

#### The vast majority of work on HPCs is done via a batch system

    #There are this many jobs running
    [davidg@bunya1 ~]$ squeue | grep " R " | wc -l
    801

    #and this many are queued
    [davidg@bunya1 ~]$ squeue | grep " PD " | wc -l
    470

We often want to know how busy Bunya is. The `sinfo` command tells us
the state of all the nodes in a partition.

    [davidg@bunya1 ~]$ sinfo -p general
    PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
    general      up 14-00:00:0      1  down$ bun009
    general      up 14-00:00:0      1  drain bun023
    general      up 14-00:00:0     39    mix bun[008,010-011,026,034,045-050,060,062,083-086,088,090,092-095,097,099-105,108-115]
    general      up 14-00:00:0     54  alloc bun[006-007,012-022,024-025,027-033,035-044,051-059,061,063-067,087,089,091,096,098,106-107]


    [davidg@bunya1 ~]$ sinfo -p gpu_cuda
    PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
    gpu_cuda     up 7-00:00:00      1  down$ bun003
    gpu_cuda     up 7-00:00:00     16    mix bun[004-005,068,071-082,116]

The node states will usually be one of

-   idle (no jobs),
-   mix (mixed, some space left for new jobs),
-   alloc (fully allocated),
-   drain (emptying, usually for maintenance),
-   down (faulty or down for maintenance)

#### There is the possibility of interactive use BUT …

Interactive use *must* still be mediated by the batch system to fairly
share the resources.

This ensures that the computation takes place on a compute nodes.

Installing R packages must *not* be done on the login nodes. Getting in
early ;-)

Interactive graphical usage of R can be achieved using

-   interactive command line jobs with X11 forwarding enabled
-   Bunya-on-demand via a web browser

So, yes, you can run RStudio. Indeed, *two* ways!

### The implications for your R code

Some of the benefits of moving to HPC are access to potentially

-   thousands of CPU cores,
-   terabytes of RAM,
-   fast temporary disk for large data sets,
-   ease of use of RDM storage for archiving data.

Some of the challenges:

-   managing your source code across platforms
-   modifications for locations
-   locating R software and pre-built libraries
-   handling the different CPU architectures
-   letting go of the notion of an all encompassing R script

### Using R on Bunya

-   There is a great deal of software installed on Bunya.
-   You just need to be able to find it!
-   Environment modules (based on lmod) does all the “dirty work”.
-   You can activate/deactivate access to installed software.
-   The central installations of R will have LOTS of “extensions” (R
    packages).
-   If you need some exotic R package, you are able to install it
    yourself.

#### How to activate R in your session

    [uqdgree5@bun048 R]$ module purge

    [uqdgree5@bun048 R]$ module load r/4.3.3-gfbf-2023a

    [uqdgree5@bun048 R]$ which Rscript
    /sw/auto/rocky8c/epyc3/software/R/4.3.3-gfbf-2023a/bin/Rscript

    [uqdgree5@bun048 R]$ cat demo.R
    1+1
    2+2
    [uqdgree5@bun048 R]$

    [uqdgree5@bun048 R]$ Rscript demo.R
    [1] 2
    [1] 4

#### Where is it going to search for R packages?

    [uqdgree5@bun048 R]$ module purge

    [uqdgree5@bun048 R]$ module load r/4.2.1-foss-2022a

    [uqdgree5@bun048 R]$ which R
    /sw/auto/rocky8c/epyc3/software/R/4.2.1-foss-2022a/bin/R

    [uqdgree5@bun048 R]$ R

    R version 4.2.1 (2022-06-23) -- "Funny-Looking Kid"
    Copyright (C) 2022 The R Foundation for Statistical Computing
    Platform: x86_64-pc-linux-gnu (64-bit)

    R is free software and comes with ABSOLUTELY NO WARRANTY.
    You are welcome to redistribute it under certain conditions.
    Type 'license()' or 'licence()' for distribution details.

      Natural language support but running in an English locale

    R is a collaborative project with many contributors.
    Type 'contributors()' for more information and
    'citation()' on how to cite R or R packages in publications.

    Type 'demo()' for some demos, 'help()' for on-line help, or
    'help.start()' for an HTML browser interface to help.
    Type 'q()' to quit R.

    [Previously saved workspace restored]

    > .libPaths()
    [1] "/home/uqdgree5/R/x86_64-pc-linux-gnu-library/4.2"
    [2] "/sw/auto/rocky8c/epyc3/software/R/4.2.1-foss-2022a/lib64/R/library"
    > q()
    Save workspace image? [y/n/c]: n

#### Remember mention of EPYC3 and EPYC4 CPUs ?

-   You can build additional R packages if you need them.
-   They install into your `R` folder in your home directory.
-   An R package built on an EPYC3 node will work on EPYC3 and EPYC4.
-   An R package built on an EPYC4 node will only work on EPYC4.

#### You don’t need to re-build any of the following packages

-   They have been built separately on EPYC3 and EPC4 nodes.
-   It will save you disk quota and time if you don’t re-build them.
-   Be careful *not* to reset your `.libPaths()` and ignore these.
-   There are almost 1200 popular R packages pre-installed with the R
    Version 4.2.1 installation on Bunya.

<!-- -->

    [davidg@bunya1 ~]$ ls /sw/auto/rocky8c/epyc3/software/R/4.2.1-foss-2022a/lib64/R/library
    abc                   doMC                ineq                      parallelly          scatterplot3d
    abc.data              doParallel          influenceR                parallelMap         scs
    abe                   doRNG               infotheo                  ParamHelpers        sctransform
    abind                 doSNOW              ini                       parsedate           SDMTools
    acepack               dotCall64           inline                    party               seewave
    adabag                downloader          intergraph                partykit            segmented
    ade4                  dplyr               interpretR                pastecs             selectr
    ADGofTest             dr                  intrinsicDimension        patchwork           sem
    admisc                drgee               inum                      pbapply             semPLS
    aggregation           DRR                 ipred                     pbivnorm            semTools
    AICcmodavg            drugCombo           irace                     pbkrtest            sendmailR

    <SNIP>                <SNIP>              <SNIP>                    <SNIP>              <SNIP>

    dismo                 HWxtest             origami                   Rvmmin              xtable
    distillery            hypergeo            orthopolynom              RWeka               xts
    distr                 ica                 osqp                      RWekajars           yaImpute
    distrEx               IDPmisc             outliers                  s2                  yaml
    distributional        idr                 packrat                   sampling            yulab.utils
    DistributionUtils     ids                 pacman                    sandwich            zeallot
    diveRsity             ie2misc             pammtools                 sass                zip
    dlm                   igraph              pamr                      SBdecomp            zoo
    DMCfun                image.binarization  pan                       scales
    doc2vec               imager              parallel                  scam
    docstring             imagerExtra         parallelDist              scatterpie
    [davidg@bunya1 ~]$

### Access Methods for R

#### Command line interactive batch job

-   As shown earlier
-   Command line based
-   Can be used to launch interactive applications
-   Key steps
    -   Login to the login node
    -   `salloc ... srun` resource request and run shell
    -   `module load ...` activate software
    -   use software

#### Regular batch jobs

-   Create R scripts that are suitable for use on Bunya
-   Create a [batch job script
    file](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#slurm-scripts)
    that will run the job
-   `sbatch jobScriptFile`

#### Bunya-on-Demand

-   Graphical user interface access to Bunya
-   Accessed via web browser
-   Select applications from the menus, or
-   Launch a terminal window
    -   `module load ...` to activate the software
    -   start the software
    -   [how it looks for
        RStudio](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/OnDemand-Guide.md#rstudio)

------------------------------------------------------------------------

### Parameter Sweeps

-   Often R code is used as part of a parameter sweep study
    -   Species of animal/plant/insect
    -   Regions of the globe
    -   Seasons of the year
    -   Climate scenarios of the future
    -   *even* crocodile ID numbers!

<!-- -->

    #How parameter sweeps get big quickly ... 1,000,000 combinations
    for (i in 0:999){
      for (j in 0:99){
        for (k in 0:9){
          do_something(i,j,k)
        }
      }
    }

Even if you do this on a Bunya node, using `library(parallel)`, you can
only perform 96 combinations in parallel.

It is often more effective to break it into smaller pieces and use a
*high throughput computing (HTC)* approach. Simplest would look like

-   strip away one of the layers of the nested for loop (e.g. i)
-   pass i parameter values in as parameters to the R script
-   use the `commandArgs` function to accept the value into your code
-   for each value of i, `Rscript scriptName.R i`

#### Job Arrays

Bunya has support for “Job Arrays” which make sweeping over integer
parameter values straightforward.

Job arrays can be adapted to sweep non-integer parameters, too.

Job arrays on Bunya are limited to 1,000 elements, but you can submit
more than one to the batch system.

#### Nimrod

UQ RCC will be adding a tool called Nimrod to Bunya later this year.

That will make it easier to sweeps over combinations of parameters that
are not integers.

Nimrod can sweep over parameters values that are

-   floating point values,
-   sets of character strings,
-   a list filenames found in a directory,
-   etc.

## In summary

*The possibilities that arise from combining R with HPC are well worth
the learning curve!*

------------------------------------------------------------------------

A recording of this presentation is available
[online](https://www.youtube.com/watch?v=62ZgQ1DWuZ8)

This document was created using R Studio 2024.04.0 Build 735 (R Version
4.4.0) and KnitR on Windows 11.

------------------------------------------------------------------------

.
