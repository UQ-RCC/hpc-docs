# Status of Major Software Installations

## Licensed Software 

### Ansys 

[**AVAILABLE**]

* Access is restricted to approved UQ EAIT users only.

* The Ansys dependencies have been built and deployed as a single *mega-module*.
* The issue with the system coupling component now appears to have been resolved following a system configuration patch.
 
To load the dependencies and set the environment for using Ansys:

`module load ansys/2023.1` 

Please submit a support request via email to rcc-support@uq.edu.au if you experience any issues with Ansys.

___
### Gurobi

[**UNAVAILABLE DUE TO LICENSE ACCESS ISSUE**]

* Version 9.5 has been installed.
* There is an ongoing issue with accessing the Gurobi product license servers on campus.
* RCC is working with the vendor to faciliate access and use of the campus license server.
* Version 10.x will be installed once the license issue is resolved. 

Watch this space!
___
### MATLAB 

#### UQ Users

[**AVAILABLE BUT UPDATES NEEDED**]

* The version of MATLAB that is available does not support some Simulink functionality.
* Updates will be installed soon.

#### Non-UQ 

[**UNAVAILABLE**]

* The access to license servers at home institutions needs to be configured.
* Once that is established, software installation can occur.
___
### Star-CCM+

[**AVAILABLE FOR TESTING**]

* Access to the UQ license server for this product has been established.
* Several dependencies have been deployed.

To test functionality please 

`module load star-ccm+/.17.02.008`

Please submit a support request via email to rcc-support@uq.edu.au if you experience any issues while testing Star-CCM+.

___
## Software Survey Requests

In late 2022, we asked users to participate in the software survey to ascertain which tools were required on Bunya.
The following table summarises the status of those requests.

_BIG TABLE_

___
## Post Software Survey Requests

These are requests that were not included in the software survey and have been requested since that time. They are necessarily lower priority.

___
## Full Module List

You should run `module overview` on Bunya to get the up-to-date list of installed software.
```
------------------------------------------------------------------- /sw/auto/rocky8.6/epyc3/modules/all --------------------------------------------------------------------
abricate           (1)   cp2k              (1)   flye        (1)   hdf5            (1)   lapack     (1)   metaeuk     (1)   prokka          (1)   spades            (1)
anaconda3          (1)   cppy              (2)   foss        (4)   hifiasm         (1)   libarchive (2)   metis       (1)   protobuf-python (2)   spectra           (1)
ansys-dependencies (1)   cuda              (2)   freebayes   (1)   hmmer           (1)   libdeflate (1)   miller      (1)   pybigwig        (1)   ssw               (1)
ant                (1)   cudnn             (2)   fsom        (1)   htseq           (1)   libgeotiff (1)   miniconda3  (1)   pybind11        (2)   star              (1)
any2fasta          (1)   cunit             (1)   gatk        (1)   htslib          (2)   libgit2    (1)   mono        (1)   pycoqc          (1)   stringtie         (1)
aocc               (1)   cutadapt          (1)   gaussian    (1)   humann          (1)   libglu     (2)   motif       (1)   pysam           (2)   suitesparse       (1)
archspec           (1)   cutensor          (1)   gcc         (4)   hypothesis      (2)   libglvnd   (2)   mpfr        (2)   python-isal     (1)   tabixpp           (1)
augustus           (1)   db                (4)   gcta        (1)   iimpi           (1)   libiconv   (1)   multichoose (1)   python          (5)   tbb               (2)
bamtools           (1)   db_file           (1)   gdal        (1)   imagemagick     (1)   libidn2    (1)   multiqc     (1)   qiime2          (1)   tbl2asn           (1)
bbmap              (1)   deeptools         (1)   gdrcopy     (2)   imkl            (2)   libint     (1)   nccl        (2)   quantumespresso (1)   tkinter           (2)
bcftools           (2)   dendropy          (1)   geos        (1)   impi            (1)   libnsl     (1)   netcdf      (1)   quast           (1)   tqdm              (1)
beagle             (1)   diamond           (1)   gfbf        (1)   intel-compilers (1)   libogg     (1)   nextflow    (1)   r               (2)   trimmomatic       (1)
bedtools           (1)   double-conversion (1)   gffcompare  (1)   intel           (1)   libtirpc   (2)   ninja       (2)   re2c            (1)   trinity           (1)
bio-searchio-hmmer (1)   easybuild         (2)   gffread     (1)   interproscan    (1)   libvorbis  (1)   nlopt       (1)   rjags           (1)   typing-extensions (1)
bioperl            (1)   elpa              (1)   ghostscript (1)   intervaltree    (1)   libxml2    (1)   openblas    (4)   ruby            (2)   ucc               (1)
biopython          (1)   expecttest        (2)   git         (2)   isa-l           (2)   libxslt    (1)   openmpi     (4)   rust            (2)   ucx-cuda          (2)
blast+             (1)   fastahack         (1)   gitpython   (1)   jags            (1)   libxsmm    (1)   openssl     (1)   salmon          (1)   unzip             (2)
blast              (1)   fastani           (1)   gnutls      (1)   jansson         (1)   littlecms  (1)   parallel    (1)   samtools        (1)   vasp              (1)
blis               (2)   fastp             (1)   go          (2)   java            (1)   lmdb       (1)   pcre2       (1)   scafacos        (1)   vcflib            (1)
boost              (2)   fastqc            (1)   groff       (3)   jbigkit         (2)   lpsolve    (1)   perl        (6)   scalapack       (4)   vcftools          (1)
bowtie2            (2)   fasttree          (1)   gromacs     (1)   jellyfish       (1)   lz4        (2)   picard      (1)   scikit-build    (1)   voro++            (1)
brotli             (2)   fermi-lite        (1)   gsl         (2)   jsoncpp         (1)   mafft      (1)   pigz        (1)   scipy-bundle    (2)   wget              (1)
busco              (1)   ffmpeg            (2)   gtdb-tk     (2)   julia           (1)   magma      (2)   pkgconfig   (1)   sdl2            (1)   x264              (2)
bwa                (1)   fftw.mpi          (1)   gtk2        (1)   kallisto        (1)   makeinfo   (2)   plink       (1)   sepp            (1)   x265              (2)
capnproto          (1)   fftw              (4)   gtk3        (1)   kim-api         (1)   mash       (1)   plotly.py   (1)   seqlib          (1)   xml-libxml        (1)
cd-hit             (1)   filevercmp        (1)   guile       (1)   kraken2         (1)   matplotlib (2)   plumed      (1)   seqtk           (1)   xvfb              (1)
cellranger         (1)   flac              (1)   gzip        (2)   kronatools      (1)   maxquant   (1)   popt        (1)   smithwaterman   (1)   xxd               (1)
checkm             (1)   flex              (1)   h5py        (1)   lame            (2)   megahit    (1)   pplacer     (1)   snakemake       (1)   yasm              (2)
cmake              (2)   flexiblas         (2)   hdf         (1)   lammps          (1)   meson      (2)   prodigal    (1)   snappy          (1)   zstd              (2)

------------------------------------------------------------------- /sw/local/rocky8.6/epyc3/rcc/modules -------------------------------------------------------------------
matlab (1)

------------------------------------------------------------------ /sw/local/rocky8.6/noarch/rcc/modules -------------------------------------------------------------------
ansys (1)   star-ccm+ (1)

------------------------------------------------------------------ /sw/local/rocky8.6/epyc3/qcif/modules -------------------------------------------------------------------
3d-dna (1)   biobakery_workflows (1)   gtdbtk (1)   mtag (1)   rmats-turbo (1)   salsa2 (1)   shovill (1)   shpc (1)

------------------------------------------------------------------ /sw/local/rocky8.6/noarch/qcif/modules ------------------------------------------------------------------
blast (1)   fastool  (1)   hisat2   (1)   kofamscan (1)   mlst        (1)   nanopolish    (1)   rsem      (1)   star         (1)   trinity   (2)   xpore (1)
f5c   (1)   gff3sort (1)   kallisto (1)   mixer     (1)   nanocompore (1)   ont-fast5-api (1)   sra-tools (1)   transdecoder (1)   trinotate (1)

```
