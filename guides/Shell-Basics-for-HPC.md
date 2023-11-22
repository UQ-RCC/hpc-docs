# Shell Basics for HPC

This document will form the basis of a workshop being offered at ResBaz Brisbane 2023.
You will be able to participate without having an active HPC account but it would be preferrable.

## Workshop Objective

_To enhance your effectiveness in using HPC by improving the resilience and utility of your HPC job scripts using shell scripting techniques._

## Assumed Knowledge
You should be familiar with command line environments. 
This [link](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#general-hpc-information)
 will provide you with access to short videos that will be of assistance.

## Pre-requisites

### Access to a HPC or linux system or an emulator

You will need access to _one_ of the following:
* A command line HPC system account would be advantageous but is not essential.
There are options for a local linux command line that will be useful for most of the session materials.
Refer to this ["Software Carpentry setup guide"](https://carpentries.github.io/workshop-template/install_instructions/#the-bash-shell)
* The Git Bash tool for Windows (advanced users might prefer to use WIndows Subsystem for Linux)   
* The Terminal app for MacOS
* A command prompt for linux

### SSH Client Tool

To connect with a remote linux system, you will need to use one of  
* Command prompt ssh command for Windows
* puTTY or MobaXterm for Windows
* the Terminal app for MacOS
* a terminal on linux

## Workshop Outline

- Getting connected to HPC (or emulating)
- What is linux shell?
- What the BASH ?!
- Features of bash that are very handy

## What the BASH ?!
  * What is BASH?
  * man bash
  * .bashrc
  * .bash_profile
  * Shell script structure
  * Executing scripts vs. Sourcing

## What are HPC job scripts?
  * Language line
  * Batch system resource directives
  * Job payload that gets run
  * A simple Bunya example

* Some issues that arise with job payloads
  * an executable that isn't
  * a data file that is missing
  * module hasn't loaded
  * you need to generate unique scripts from a template
    
* How to write a templating script
* Basic templating techniques
*  
