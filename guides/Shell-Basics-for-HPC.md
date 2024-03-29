# Shell Basics for HPC

## Workshop Objective
_Learn how to enhance your effectiveness in using high-performance computing (HPC) resources, by improving the resilience and utility of your HPC job scripts using shell scripting techniques._

## Workshop Background
This document will form the basis of a workshop being offered at ResBaz Brisbane 2023.
You will be able to participate without having an active HPC account but it would be preferrable.

## Assumed Knowledge
You should be familiar (though not expected to be experts) with command line linux environments. 
This [link](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#general-hpc-information) will provide you with access to short videos that will be of assistance.

## Pre-requisites

### Access to a HPC or linux system or an emulator

You will need access to _one_ of the following:
* A command line HPC system account would be advantageous but is not essential.
There are options for a local linux command line that will be useful for most of the session materials.
Refer to this [Software Carpentry setup guide](https://carpentries.github.io/workshop-template/install_instructions/#the-bash-shell)
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

- Getting ourselves connected to HPC (or emulating same)
- What the BASH ?!
- Features of bash that are very useful
- Some scenarios that benefit from shell scripting.
- If time permits, we'll look at what is giving your trouble in job scripts.

## What the BASH ?!
### What is BASH?
* Bourne Again SHell (bash) is an improvement on the original Bourne SHell (sh)
* BASH is one of several linux/unix shells e.g. csh tcsh ksh zsh
* A shell is the outer lay that wraps the operating system kernel, drivers and hardware to allow the user to do things.
* It provides command line interactivity with the operating system. 
* See ``man bash`` for details. ``-l`` (or ``--login``) is an important option on Bunya HPC.
* .bashrc and .bash_profile

### (Typical) shell script structure
* Language line
* Mix of Comment lines and linux commands that get run sequentially (unless you use backgrounding)

### [Pipes](https://swcarpentry.github.io/shell-novice/04-pipefilter.html) vs. [Scripts](https://swcarpentry.github.io/shell-novice/06-script.html)
* Output from a command can be piped into another command. Makes for powerful, but linear operations.
* Scripts have more overhead but provide flow control that you don't get with pipes.
  
### Executing scripts vs. Sourcing
* executing a script "forks" a new process that runs the contents of the shell script.
* sometimes you want to modify your current environment (so use ``source mySettings`` or ``. mySettings``

## What are HPC job scripts?
* Language line
* Batch system resource directives (funky comment lines near the top)
* Job payload that gets run
* A simple Bunya example

## Shell language features
* ``$ENVIRONMENT_VARIABLES``
* special cryptic environment variables ``$0`` (script local) ``$1`` (first command line argument) ``$2`` (second command line argument) ``$*`` (all command line arguments) ``$!`` ``$$`` (process id) 
* arrays (bash and a couple of the other shells)
* tests  using ``test -x myCode`` or ``[ -x myCode ]`` 
* ``if then else elif fi`` blocks
* ``case`` statements are like a switch in C language
* ``for`` and ``while`` [loops](https://swcarpentry.github.io/shell-novice/05-loop.html)
* functions (for more reusable code)

## Some of the linux command line power tools ([aka filters](https://swcarpentry.github.io/shell-novice/04-pipefilter.html))
* ``sort`` and ``uniq``
* ``find``
* ``grep`` ``sed`` and ``awk``
* ``tr``
* ``cut``
* ``bc`` and ``expr``

## Some situations that are enhanced by the use of some shell scripting
  * issues that arise with job payloads
  * an executable that isn't
  * a data file that is missing
  * a module hasn't loaded
  * you need to generate individual scripts from a template
  * basic templating techniques

## Think, and test, before you fire a shell script at the HPC 

