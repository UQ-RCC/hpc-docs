# Conda, conda installs and conda environments

## Advice on user installed conda

The advice to users is to avoid running the conda initialisation which writes to the user's `.bashrc` file. This changes the user's shell permanently and can cause problems. If your prompt has a `(base)` attached to it when you log in then your `.bashrc` file has already been changed. You can reverse this by cleaning up your `.bashrc` file and sourcing the `conda.sh` file from your installation. Users can then use<br>
`source activate`<br> 
to switch on the conda base environment and<br>
`conda deactivate` <br>
to switch it off again.
This is keeping the shell clean and conda base and other conda environments can so be loaded for jobs only.

Users can clean their `.bashrc` file by opening it and removing everything between and including these two lines<br>
`# >>> conda initialize >>>`<br>
`# <<< conda initialize <<<`<br>

Users can also clean their `.bashrc` file by using `conda init` again with <br>
`conda init --reverse`<br>


## Advice on conda and Open OnDemand usage

If you have the conda initialisation in your `.bashrc` file then you cannot use Open OnDemand. To use the virutal desktop in Open OnDemand you need to have clean `.bashrc` file. The easiest was to clean it is to run <br>
`conda init --reverse`<br>


## Using a conda module

### Bunya

There is no need to install Anaconda3 or Miniconda3 yourself. Both are available as modules on Bunya. 

Please load the relevant module. 

```
anaconda3/2022.05
miniconda3/4.12.0
```
Then set up your shell to use the chosen conda version. Using the environmental variables `$EBROOTANACONDA3` or `$EBROOTMINICONDA3` will ensure that you pick the correct one on any node architecture. This is important as the paths to the installation can differ on compute nodes with different architecture. It also means it will still work no matter wich version of anaconda3 or miniconda3 you loaded.

`source $EBROOTANACONDA3/etc/profile.d/conda.sh`<br>
or<br>
`source $EBROOTMINICONDA3/etc/profile.d/conda.sh`<br>

Now your shell is ready to create a conda environment.

### Wiener

Anaconda2 and Anaconda3 are available on Wiener.

```
anaconda/2.7
anaconda/3.5       
anaconda/3.6 
anaconda/3.7
```

The set up your shell to use the chosen conda version. The easiest way to do this on Wiener is to use this line (this is broken for anaconda/3.5):

`eval "$(conda shell.bash hook)"`

This will automatically activate the `(base)` conda environment without changing your `.bashrc` file. To deactivate the `(base)` environment just use

`conda deactivate`

Now your shell is ready to create a conda environment.

## Base conda environment

If you want to activate the base conda environment you can do<br>
`[username@bunya3 ~]$ conda activate`<br>
`(base) [username@bunya3 ~]$`<br> 

And to get out of the base conda environment you can do<br>
`(base) [username@bunya3 ~]$ conda deactivate`<br>
`[username@bunya3 ~]$`<br>

This also works on Wiener.

## Creating a new conda environment

1. Here we are creating a conda environment called `myenv` which you can replace by a name more relevant to you<br>
`conda create --name myenv`

Please note: By default environments are installed into the `envs` directory in your conda directory which is `/home/YourUsername/.conda`. If you need to specify a particular location for an environment please have a look [here](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#specifying-location).

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

## Changing the location of conda environments and package caches

On Bunya the home directory has 50GB of space and 1 million files to allow installation of environments. However, in case this is to install shared environments into `/scratch` which is also needed on Wiener, this is an easy way to do this.

The home directoy on Wiener is very small (5GB) and it is advised to install conda environments into scratch.  To have this setup so environments are installed in a different location automatically and also found it is best to use the [Conda configuration file](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html), `.condarc`.
See specifically instructions on envs location [here](https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html#specify-environment-directories-envs-dirs).

In your home directory open the `.condarc` file. You can use `nano` for this or `vi`, what ever you are comfortable with.

The insert these lines:

```
envs_dirs:
  - /scratch/rest-of-the-path-of-location/envs
```
Or you can do 

```
cat << EOF >> $HOME/.condarc

```
You will see a `>` once you pressed the enter key. Now enter these lines (you can copy and paste)

```
envs_dirs:
   - /scratch/rest-of-the-path-of-location/envs
EOF

```
The should return you (the `>` should disappear). If not press the enter key again.

Check that the lines have been added by typing

`cat $HOME/.condarc`

On Bunya the location for the environments can be

`/scratch/user/username/rest-of-path/envs`

or

`/scratch/project/project-name/rest-of-path/envs`

On Wiener the location can be 

`/scratch/my-org/username/rest-of-path/envs`

This will allow you to install environments and find them by name. You will not need the full path to activate the environment.

## Activating a conda environment

`conda activate myenv`

## Deactivating a conda environment

`conda deactivate myenv`

For further information on conda environments please go [here](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#).












