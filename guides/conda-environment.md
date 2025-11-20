# Conda, Conda modules and Conda environments

Conda is a Python environment and package manager. It supports isolated environments and allows you to manage dependencies for different Python projects
without interfering with system-wide packages or each other. It also provides a large set of precompiled binaries for applications such as Tensorflow, PyTorch,
NumPy, Pandas, bioinformatics and genomics software, and many more.

## Important warning on user installed Conda

>[!IMPORTANT]
>The advice to users is to avoid running the Conda initialisation which writes to the user's `.bashrc` file. This changes the user's shell permanently and can cause problems. If your prompt has a `(base)` attached to it when you log in then your `.bashrc` file has already been changed. You can reverse this by cleaning up your `.bashrc` file and sourcing the `conda.sh` file from your installation. Users can then use<br>
>`conda activate`<br> 
>to switch on the Conda base environment and<br>
>`conda deactivate` <br>
>to switch it off again.
>This is keeping the shell clean and Conda base and other Conda environments can so be loaded for jobs only.
>
>Users can clean their `.bashrc` file by opening it and removing everything between and including these two lines<br>
>`# >>> conda initialize >>>`<br>
>`# <<< conda initialize <<<`<br>
>
>Users can also clean their `.bashrc` file by using `conda init` again with <br>
>`conda init --reverse`<br>


## Important warning on user installed Conda and onBunya usage

>[!IMPORTANT]
>If you have the conda initialisation in your `.bashrc` file then you cannot use onBunya. To use the virutal desktop in onBunya you need to have clean `.bashrc` file. The easiest was to clean it is to run <br>
>`conda init --reverse`<br>

## Important warning to not run installs on login nodes
>[!IMPORTANT]
>**ALL** software builds should be done on a compute node. Processes running on the login nodes, including software builds (conda environments, make-make install, EasyBuild) will most likley be killed if found on the login nodes.
>
>If you are building your own software, especially if you are compiling your own software, you need to be aware of the different architectures, `epyc3` and `epyc4`. Software built on an `epyc3` compute node will run on a `epyc4` compute node **BUT** software built on a `epyc4` compute node will not run on a `epyc3` compute node. If you want ease of use you need to make sure to compile on a `epyc3` compute node. If you want best performance you should compile for a specific architecture but then need to request that architecture for your jobs.
>See here (https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#interactive-jobs) for how to submit an interactive job.

## Using existing Conda modules

There is no need to install Conda yourself. Several Conda modules are available on Bunya for managing Python environments.

- `miniforge`
- `anaconda3`
- `miniconda3`
  

### Miniforge features
- Miniforge includes the `mamba` command in addition to `conda`.
- `mamba` is a drop-in replacement for `conda`, offering faster dependency resolution. The two commands are interchangeable.
- Environments created with `mamba` are still referred to as **Conda** environments and follow the same configuration methods.
- By default, Miniforge uses the `conda-forge` channel for package management.  

Several versions of Anaconda3, Miniconda3, and Miniforge, are available as modules on Bunya. Use 
`module avail anaconda miniconda miniforge` 
to check on current versions available.


```
anaconda3/2022.05
anaconda3/2023.09-0
miniconda3/4.12.0
miniconda3/23.9.0-0
miniforge/24.3.0-0
miniforge/24.11.3-0
```

Please load the relevant module by using the full name and version.

Then set up your shell to use the chosen Conda version. Using the environmental variables `$EBROOTANACONDA3`, `$EBROOTMINICONDA3`, or `$ROOTMINIFORGE` will ensure that you pick the correct one on any node architecture. This is important as the paths to the installation can differ on compute nodes with different architecture. It also means it will still work no matter which version of anaconda3, miniconda3, or miniforge you loaded.

`source $EBROOTANACONDA3/etc/profile.d/conda.sh`<br>
or<br>
`source $EBROOTMINICONDA3/etc/profile.d/conda.sh`<br>
or<br>
`source $ROOTMINIFORGE/etc/profile.d/conda.sh`<br>

Now your shell is ready to use, create, and modify a Conda environment.


## Base Conda environment

Conda environments are self-contained spaces that contain the software and dependencies needed to run your Python applications.

If you want to activate the base Conda environment you can do<br>
`[username@bunya3 ~]$ conda activate`<br>
`(base) [username@bun-node ~]$`<br> 

And to get out of the base Conda environment you can do<br>
`(base) [username@bun-node ~]$ conda deactivate`<br>
`[username@bun-node ~]$`<br>

## Changing the default location of Conda environments and package caches

By default, Conda stores environments and downloaded package files in your home directory (`/home/username/.conda/`). These files can quickly consume a significant amount of storage, especially when working with machine learning libraries, GPU-enabled packages or bioinformatics software with data sets. On Bunya the home directory has 50GB of space and 1 million files to allow installation of software environments.

Users should check `/scratch/opendata` first for available data sets and models before installing a copy themselves.

However, in cases where there is a need to install Conda environments and/or packages into a different location such as `/scratch/user/username`, or `/scratch/project/projectname` the default location for Conda environments and/or packages can be changed.

To change the default location update Conda's configuration edit `~/.condarc`
and ensure it contains these lines:

```
envs_dirs:
  - /scratch/user/username/conda/envs

pkgs_dirs:
  - /scratch/user/username/conda/pkgs
```
or

```
envs_dirs:
  - /scratch/project/projectname/conda/envs

pkgs_dirs:
  - /scratch/project/projectname/conda/pkgs
```

Alternatively, these commands will set the default locations:

```
conda config --set envs_dirs /scratch/user/username/conda/envs
conda config --set pkgs_dirs /scratch/user/username/conda/pkgs
```
or

```
conda config --set envs_dirs /scratch/project/projectname/conda/envs
conda config --set pkgs_dirs /scratch/project/projectname/conda/pkgs
```

After making these changes:
- New environments will be created in `/scratch/user/username/conda/envs` or `/scratch/project/projectname/conda/envs`.
- Downloaded package files will be stored in `/scratch/user/username/conda/pkgs` or `/scratch/project/projectname/conda/pkgs`.

> [!Note]
> Any existing environments and cached packages in `/home/username/.conda/` will remain there unless they are moved manually or recreated in the new location.

> [!Caution]
> The automatic purging of unused files in /scratch after 90 days commenced in November 2025.
> If you relocate your envs directory to /scratch it will be subject to automatic deletion. Files within an otherwise active conda environment may be silently deleted.
> See the [section below](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/conda-environment.md#future-proofing-your-envs) about some options about what to do.

## Conda channels

Conda channels are repositories that host precompiled packages.

### Defaults channel

By default, Conda pulls packages from the `defaults` channel, maintained by Anaconda, Inc. Packages available in `defaults` are curated by Anaconda Inc. who prioritise
stability and compatibility. Some applications may also include commercial or proprietary optimisations.

### Conda-Forge channel

`conda-forge` is a community-driven open-source channel. It offers a broader selection of packages, which are generally more up to date that those in `defaults`. For most use cases `conda-forge` is recommended due to its broader package selection and frequency of updates.

### Other channels

Other channels are available such as:
- `bioconda` – bioinformatics and genomics software
- `nvidia` – GPU-accelerated libraries
- `pytorch` – official PyTorch packages

These channels should be used as needed on a case-by-case basis. In most cases, the required packages can be found on `conda-forge`, but certain specialized
packages may only be available in specific channels.

> [!NOTE]
> Installing packages, such as GPU-accelerated libraries, can usually be done using the `conda-forge` channel. A specialised channel such as `nvidia`, should be used when there is a special need to do so.
> Most bioinformatics packages can usually be done using the `conda-forge` and `bioconda` channels.

## Creating a new Conda environment

1. Here we are creating a Conda environment called `myenv` which you can replace by a name more relevant to you<br>
`conda create --name myenv`

This creates an empty environment with no installed packages except Conda itself.

Please note: By default environments are installed into the `envs` directory in your Conda directory which is `/home/username/.conda` unless the default location has been changed, see above.

2. When Conda asks you to proceed type `y`

3. To create an environment with a specific python version, for example python 3.9:<br>
`conda create --name myenv python=3.9`

4. To create an environment with a specific package, for example scipy:<br>
`conda create --name myenv scipy`<br>
or<br>
`conda create --name myenv`<br>
`conda install --name myenv scipy`<br>

5.  To create an environment with a specific version of Python and multiple packages:<br>
`conda create --name myenv python=3.9 scipy=0.17.3 astroid babel`

Tip: Install all the programs that you want in this environment at the same time. Installing 1 program at a time can lead to dependency conflicts.

## Activating a Conda environment

`conda activate myenv`

You can also activate environments outside your default location by specifying its full path:

```
conda activate /scratch/project/projectname/myenv
```

After activating an environment Python will use the packages and dependencies installed within it.

To check which environment is currently active and get other useful information run:
```
conda info
```

## Modifying a Conda environment

When an environment is active packages can be modified with Conda commands such as:

```
conda install <package>
conda update <package>
conda remove <package>
```

## Deactivating a Conda environment

`conda deactivate myenv`

Environments must be deactivated before they can be deleted using Conda.

## Removing a Conda environment

Remove an environment in your default location by running:

```
conda env remove --name myenv
```

After removing an environment, clearing your Conda cache can be used to free up disk space and remove package files that are no longer needed. To do this, run:

```
conda clean --all
```

This command will:

- Remove unused package tarballs from the package cache.
- Clear extracted package files.
- Remove temporary Conda files and logs.

For further information on Conda environments please go [here](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#).

## Using Pip

Pip can be used to install local packages (e.g., locally built) or packages that are not available from Conda channels. Pip packages can be installed alongside Conda packages, but it is also useful to install Pip packages in an empty Conda environment to make use of Conda's facilities such as:
- Installing specific Python versions
- Package isolation
- Removing environments including packages and dependencies

### Mixing Pip and Conda packages

Although it is not recommended to mix Pip and Conda packages, it is possible to do so by following these rules:
- Ensure the Conda environment is activated before using Pip.
- **Always** install the required Conda packages first.
- Avoid modifying the environment with Conda commands after installing packages with Pip as it may cause issues. Removing and re-creating the environment is generally the best way to fix any problems created.

### Using Pip packages exclusively
> [!CAUTION]
> It is important **not** to install pip packages in 'bare' or 'empty' Conda environments. Doing so can lead to problems with package paths.

A Conda environment with no Conda packages installed is known as a 'bare' or 'empty' environment. Creating an environment using the following command will result in a bare environment.

```
conda create --name myenv-for-pip
```
Before an environment can be used for installing Pip applications it must be 'populated' by installing Python. Specifying `python` when creating the Conda environment will install Python automatically:

```
conda create --name myenv-for-pip python=3.10
```

This will create a populated Conda environment `myenv-for-pip` with Python 3.10, ready to install pip applications.


## Future proofing your envs

It is possible to work within the fixed /home quota and /scratch 90 day deletion.

There are some options available to you to future proof your access to conda environments:
* use, where ever possible, conda environments that are already available via the modules mechanism,
* if your particular conda environment is something that would be of use to other on the Bunya HPC, you could request that it be installed into /sw and made available via modules,
* if you lead a research group that all use the same set of tools, but they require frequent updates, or group specific customisations, then we could make create a space within /sw for you to manage those installations on behalf of the group,  
* you could periodically clone the aging conda environments from /scratch into /home and <br>
`conda create -p ~/envs/envname --clone oldenvname`
* you could create a tar file of your conda environments (collectively or individually) and copy the tar file to RDM for safe keeping.

The RCC team are exploring some other options to make managing conda environments more straight forward and will update our documentation in due course.














