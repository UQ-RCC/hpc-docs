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
`(base) [username@bunya3 ~]$`<br> 

And to get out of the base Conda environment you can do<br>
`(base) [username@bunya3 ~]$ conda deactivate`<br>
`[username@bunya3 ~]$`<br>

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

## Deactivating a Conda environment

`conda deactivate myenv`

For further information on Conda environments please go [here](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#).












