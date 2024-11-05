MPI calculations should be started with `srun` as using `mpirun` (and similar) does not work and can produce some unexpected and undesired behaviour. 
Therefore the `salloc` and the `srun` part need to be done seperately for interactive MPI jobs.

**Please note that interactive MPI should be restricted to a single node and that multi node testing can be done via the `debug` partition.**

First, the resources need to be requested via `salloc`:

```
salloc --nodes=1 --ntasks-per-node=96 --ntasks-per-core=1 --ntasks=96 --mem=500G --job-name=MPI-test --time=05:00:00 --partition=general --qos=normal --account=AccountString
```
Resources should be modified to be appropriate for your job as the example is asking for a full node on Bunya. It is important to keep `--ntasks-per-core=1`. 
Only ever change this if you know exactly what you are doing and how to combine MPI with OpenMP.

The `salloc` command will assign resources only, it will NOT get you to a compute node, you are still on one of the login nodes at this stage. To check you can 
always type `hostname` and if it comes back with `bunya1`, `bunya2`, or `bunya3` you are still on a login node. To actually start the 
job and get to a compute node you need to load any needed modules first and then use `srun`.

```
module load YOUR_REQUIRED_MODULES
srun --ntasks=[number up to 96] --export=ALL executable < input> output
```

You can use any number of cores you need up to the full 96 you requested via `salloc`. You need the
`--export=ALL` to export the environment with the loaded modules to the job. The `--export=ALL` will only work for the `general` and `debug` partition as its 
nodes have a similar environment and module path to the login nodes. The GPU nodes are different and you might need to use the `--export` flag to export a long 
list of variables. None of this has been tested on any of the GPU nodes.   


Executing the `srun` command will start the job. Once it is done or crashed you get your prompt back but you are still in the `salloc` allocation, 
so you are able to submit more under that allocation. To exit and release the job allocation type `exit`.

So please be very mindful that you are doing a 2 step process here, asking for an allocation (`salloc`) and then using that allocation for a calculation (`srun`). 
 
