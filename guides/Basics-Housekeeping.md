# Basics of Housekeeping on HPC

`under construction 20260305`

## Saving work to RDM

Please refer to our User Guide about [Bunya Storage](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-UserData-Guide.md)

Currently, RDM storage allocations are initially limited to 1TB and 1M files.
The TB limit is a soft limit, so you can go over it without realising so.
The files limit, however, has a hard limit at 10% above.
This means that when you transfer files into RDM Q storage, things may start to go wrong once you get to the 1M files mark.

If you suspect you 

### Scenario 1: Large numbers of file

So you are transferring a large number of files over to the RDM using rsync. 
That is, you are copying the data to RDM file-by-file. 
This is a _not_ best practice and it is an inefficient way to work with the archival storage infrastructure.
The RDM Q storage works best in "streaming" mode, and worse with a lot of little pieces of data.

Instead, of using rsync, your should bundle files into uncompressed archive files (using `tar` or `zip -0` commands, with recursion)

These uncompressed archive files are 
•	very fast to create, 
•	very easy to move around and copy back from RDM Q archives
•	very fast to read and unpack.

Create them in /scratch and copy them across to RDM when completed.

I did this recently for _very_ difficult dataset that had 3.5 million files in a single folder on /scratch!
I chunked it into about (approx) 60GB tar files with exactly 50,000 files in each.

Your directory structure would lend itself to creating archives easily.
