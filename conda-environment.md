# Conda, conda installs and conda environments

## Advice on user installed conda

The advice to users is to avoid running the conda initialisation which writes to the user's `.bashrc` file. This changes the user's shell permanently and can cause problems. If your prompt has a `(base)` attached to it when you log in then your `.bashrc` file has already been changed. You can reverse this by cleaning up your `.bashrc` file and sourcing the `conda.sh` file from your installation. Users can then use<br>
`conda activate`<br> 
to switch on the conda base environment and<br>
`conda deactivate` <br>
to switch it off again.
This is keeping the shell clean and conda base and other conda environments can so be loaded for jobs only.

## Using a conda module

There is no need to install Anaconda3 or Miniconda3 yourself. Both are available as modules. Anaconda2 as a module is coming soon.

Please load the relevant module

`module load anaconda3/2022.05`<br>
or <br>
`module load miniconda3/4.12.0`<br>

Then set up your shell to use the chosen conda version

`source /sw/auto/rocky8.6/epyc3/software/Anaconda3/2022.05/etc/profile.d/conda.sh`<br>
or<br>
`source /sw/auto/rocky8.6/epyc3/software/Miniconda3/4.12.0/etc/profile.d/conda.sh`<br>

You can also use the environment variables set by the module:

`source $EBROOTANACONDA3/etc/profile.d/conda.sh`<br>
or<br>
`source $EBROOTMINICONDA3/etc/profile.d/conda.sh`<br>

to set this up independent of the version of the Anaconda3 or Miniconda3.

Now your shell is ready to create a conda environment.

## Base conda environment

If you want to activate the base conda environment you can do<br>
`[username@bunya3 ~]$ conda activate`<br>
`(base) [username@bunya3 ~]$`<br> 

And to get out of the base conda environment you can do<br>
`(base) [username@bunya3 ~]$ conda deactivate`<br>
`[username@bunya3 ~]$`<br>

## Creating a new conda environment

1. Here we are creating a conda environment called `myenv` which you can replace by a name more relevant to you<br>
`conda create --name myenv`

Please note: By default environments are installed into the `envs` directory in your conda directory which is `/home/YourUsername/.conda`. If you need to specify a particular location for an environment please have a look [here](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#specifying-location)

2. When conda asks you to proceed type `y`

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

## Activating a conda environment

`conda activate myenv`

## Deactivating a conda environment

`conda deactive myenv`

For further information on conda environments please go [here](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#).












