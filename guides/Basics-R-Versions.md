# R Versions on Bunya

**TO BE COMPLETED**

David Green 07/11/2025
  
## What is R?
R is a programming language that developed out of statistical computing and data analysis. It has been enhanced with thousands of packages for a wide variety of computational work.
It continues to be a popular choice amongst Bunya users for simulations and analysis.

## Why so many versions on Bunya?

Refer to the Bunya User Guide section about software modules.

### Older Bare Metal Versions
When Bunya was first launched we provided R built using our centralised build system. The following versions included the core R system as well as a number of useful additional packages.
```
r/4.1.0-foss-2021a
r/4.2.1-foss-2021a
r/4.2.1-foss-2022a
```
### Newer Bare Metal Versions

The build mechanism changed for R 4.3 and R 4.4.0. 
The additional packages (numbering approximately 1,200) were built as separate items.
```
r/4.3.3-gfbf-2023a
r/4.4.0-gfbf-2023a
r/4.4.0-combo-EPYC3-only
```
Unfortunately, the `r/4.4.0-gfbf-2023a` installation was incomplete. The 1,200 or so additional packages did not build for EPYC4 CPUs. If you do choose to use this version, then you may need to build a great many packages for yourself.<br>
**I recommend that you avoid using `r/4.4.0-gfbf-2023a`.**

If you target the older EPYC3 CPU nodes, you can use the purpose built `r/4.4.0-combo-EPYC3-only`

### Software container versions

Please refer to the [*Basics.apptainer*](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Basics-apptainer.md) for information about software containers. *Software containers do not run on login nodes.*

The R programming language underpins the integrated development environment (IDE) called RStudio.<br>
Since the launch of onBunya, the RStudio software (and R within) are provided on Bunya as software containers. There are several versions available.

If you need to use a software container version of R without RStudio that is OK. The following software modules use the RStudio containers to provide access to the R version within.

|Module Name|Features|
|:------------|:------|
|`r/4.4.1`|Software container with approximately 1,200 popular R packages from CRAN.|
|`r/4.4.2`|Software container with approximately 1,200 popular R packages from CRAN.|
|`r/4.4.2-heavy`|Software container with approximately 25,000 R packages from CRAN. Requires >16GB of RAM|
|`r/4.5.1`|Software container with approximately 1,200 popular R packages from CRAN.|


>[!CAUTION]
If you use a bare metal R 4.4.x version and switch to a software container 4.4.x version, then you should delete your personal library space for that version e.g. `$HOME/R/x86_64-pc-linux-gnu-library/4.4/` and rebuild all your personal modules.




## How to access R?

### Using R within RStudio in onBunya

The RStudio software is available via the applications menu in the onBunya graphical desktop service.

### Using R within a command terminal in onBunya

Launch a terminal within onBunya.<br>
Use a `module load` of the appropriate R version you require.<br>
The commands, R and Rscript, will be automatically found in your path.

### Using R in an interactive batch job

Use a `module load` of the appropriate R version you require.<br>
The commands, R and Rscript, will be automatically found in your path.

### Using R in a regular batch job

Use a `module load` of the appropriate R version you require in your job script.<br>
The commands, R and Rscript, will be automatically found in your path.

## Problems with accessing /QRISdata from container versions of R.

Yes this is an issue. When you launch a software container you do so as your default group which won't be allowed to access your RDM data.
