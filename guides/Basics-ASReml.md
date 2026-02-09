# Using ASReml-R and ASReml-SA on Bunya HPC

`under construction  20260209`


## ASReml-R

[ASReml-R](https://vsni.co.uk/software/asreml-r/) is a statistical analysis software package for linear mixed models. 
Individuals can install ASReml-R as a personal software package into their R or RStudio environment on Bunya HPC. 

### How to setup ASReml-R for yourself

There is a very useful CRAN R package from the University of Adelaide, South Australia, called [biometryassist](https://cran.r-project.org/package=biometryassist) 
The biometryassist package will handle the installation of ASReml-R for you by providing an R function called `install_asreml()`.

```
#Install the biometryassist package once.
install.packages("biometryassist")
#Load the package
library(biometryassist)

#Install the ASReml R package
install_asreml(check_version="FALSE")  #Must not check for newer version, it will fail
#Load the asreml R package
library(asreml)

#Contact RCC Support before attempting the following steps
#Activate and test the license
asreml.license.activate()
asreml.license.status()
```

## ASReml-SA
[ASReml-SA](https://vsni.co.uk/software/asreml-sa/) is a stand alone version of ASReml.  
ASReml-SA is available via the modules mechanism on Bunya HPC. 
ASReml-SA should not and cannot be run on login nodes (it is a software container).
Please use a regular batch job, or for interactive use an interactive batch job or onBunya session.

## Licensing
The software is licensed. Please contact rcc-support@uq.edu.au regarding licensing.
