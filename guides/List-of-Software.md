# List of Additional Software on Bunya

**Updated: 19 June 2025**

The operating system installations on Bunya nodes are relatively lightweight.
This is done for a variety of sound technical reasons.

Most software, even some things that would normally be considered part of the standard operating system, are installed separately.
Access to this software is facilitated by the *modules* mechanism.
Some software is made available through GUI menus in [onBunya](https://onbunya.rcc.uq.edu.au)

For more information, please refer to these documents
- [Bunya User Guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-User-Guide.md#software)
- [Software Status](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Software-Status.md)


Most of the software listed here is freely available to use. 
Some software requires agreement to license conditions and/or authorised membership of a special access group.

>[!NOTE]
>
>These lists have been created on login nodes.
>
>Software built under /sw/auto will have an architecture specific installation location (login nodes are "epyc3").<br>
>Software built under /sw/local will only be available on the architectures where they have been installed (e.g. "epyc3" but not "epyc4").<br>
>Software built under /sw/local/.../noarch can be used on any architecture that makes sense to use. <br>
The noarch software is either provided by software containers, or, is a commercial software product (e.g. MATLAB).<br>
>GPU nodes will have additional software for utilising (e.g. CUDA for NVidia GPU nodes) and GPU specific software.

## Overview List 

This list is grouped by installation branch. 

It shows the name of the module and the number of distinct versions available.

```
---------------------- /sw/auto/rocky8c/epyc3/modules/all ----------------------
abricate              (1)   gtdb-tk         (1)   ncbi-vdb           (2)
alsa-lib              (1)   gtk2            (1)   ncurses            (8)
anaconda3             (2)   gtk3            (2)   netcdf             (3)
ansys-dependencies    (1)   guile           (1)   nettle             (3)
ant                   (2)   gzip            (3)   networkx           (3)
any2fasta             (1)   h5py            (1)   nextflow           (2)
archive-zip           (1)   harfbuzz        (3)   nghttp2            (1)
archspec              (2)   hatchling       (1)   nghttp3            (1)
armadillo             (1)   hdf             (3)   ngs                (1)
arpack-ng             (1)   hdf5            (3)   ngtcp2             (1)
at-spi2-atk           (2)   help2man        (4)   ninja              (4)
at-spi2-core          (2)   hifiasm         (1)   nlohmann_json      (2)
atk                   (2)   highway         (1)   nlopt              (3)
augustus              (2)   hipsycl         (1)   nodejs             (3)
autoconf              (5)   hisat2          (2)   nspr               (3)
automake              (5)   hmmer           (2)   nss                (3)
autotools             (5)   htseq           (1)   numactl            (5)
bamtools              (2)   htslib          (3)   openbabel          (2)
bbmap                 (2)   humann          (1)   openblas           (4)
bcftools              (3)   hwloc           (4)   openexr            (1)
bcl2fastq2            (1)   hypothesis      (3)   openjpeg           (2)
beagle-lib            (2)   icu             (3)   openmpi            (4)
beagle                (1)   iimpi           (4)   openpgm            (2)
beautifulsoup         (1)   imagemagick     (3)   openssl            (2)
bedtools              (2)   imath           (1)   p11-kit            (1)
binutils              (9)   imkl-fftw       (3)   pandoc             (1)
bio-db-hts            (1)   imkl            (4)   pango              (3)
bio-searchio-hmmer    (2)   impi            (4)   parallel           (2)
bioperl               (2)   intel-compilers (4)   patchelf           (1)
biopython             (2)   intel           (4)   pcre               (3)
bison                 (5)   interproscan    (1)   pcre2              (3)
blast+                (2)   intervaltree    (1)   perl-bundle-cpan   (1)
blast                 (1)   intltool        (3)   perl               (7)
blat                  (1)   ipython         (2)   picard             (1)
blis                  (4)   isa-l           (2)   pigz               (2)
boost.python          (2)   jags            (1)   pillow             (2)
boost                 (3)   jansson         (1)   pixman             (3)
bowtie                (1)   jasper          (3)   pkg-config         (2)
bowtie2               (2)   java            (1)   pkgconf            (5)
brotli                (3)   jbigkit         (3)   pkgconfig          (1)
brunsli               (1)   jellyfish       (2)   plink              (1)
busco                 (2)   jemalloc        (3)   plotly.py          (2)
bwa                   (2)   json-c          (1)   plumed             (3)
bzip2                 (4)   jsoncpp         (1)   pmix               (4)
c-ares                (1)   judy            (1)   pocl               (1)
cairo                 (3)   julia           (1)   poetry             (1)
canu                  (2)   jupyter-server  (1)   popt               (1)
capnproto             (1)   jupyterlab      (1)   postgresql         (1)
catch2                (1)   kallisto        (2)   pplacer            (1)
cd-hit                (2)   kim-api         (2)   prodigal           (2)
cellranger-arc        (1)   kraken2         (2)   proj               (3)
cellranger            (1)   kronatools      (1)   prokka             (2)
cereal                (1)   lame            (3)   prrte              (1)
cffi                  (1)   lammps          (2)   pybigwig           (2)
cfitsio               (1)   lapack          (1)   pybind11           (3)
checkm-database       (1)   lerc            (1)   pycoqc             (1)
checkm                (2)   libaio          (1)   pysam              (2)
clang                 (3)   libarchive      (4)   python-bundle-pypi (1)
cmake                 (6)   libcerf         (2)   python-isal        (2)
compress-raw-zlib     (1)   libdeflate      (2)   python             (8)
coordgenlibs          (2)   libdrm          (3)   pyyaml             (2)
cp2k                  (2)   libepoxy        (2)   qhull              (4)
cppy                  (2)   libev           (1)   qiime2             (1)
cryptography          (1)   libevent        (4)   qt5                (3)
cunit                 (1)   libfabric       (4)   quantumespresso    (2)
curl                  (4)   libffi          (4)   quast              (2)
cutadapt              (2)   libgd           (2)   r                  (5)
db                    (2)   libgeotiff      (3)   rapidjson          (2)
db_file               (2)   libgit2         (3)   re2c               (3)
dbd-mysql             (1)   libglu          (5)   rjags              (1)
dbus                  (3)   libglvnd        (3)   ruby               (2)
deeptools             (2)   libiconv        (3)   rust               (3)
dendropy              (2)   libidn          (2)   salmon             (2)
diamond               (2)   libidn2         (2)   samtools           (4)
double-conversion     (3)   libint          (2)   scafacos           (2)
doxygen               (3)   libjpeg-turbo   (3)   scalapack          (3)
easybuild             (4)   libnsl          (1)   scikit-build       (2)
eigen                 (3)   libogg          (3)   scipy-bundle       (3)
elfutils              (2)   libopus         (2)   sdl2               (2)
elpa                  (2)   libpciaccess    (4)   sepp               (2)
expat                 (3)   libpng          (3)   seqlib             (1)
fastahack             (1)   libpsl          (1)   seqtk              (2)
fastani               (1)   libreadline     (4)   setuptools-rust    (1)
fastp                 (1)   libsndfile      (3)   smithwaterman      (1)
fastqc                (1)   libsodium       (2)   snakemake          (2)
fasttree              (1)   libsoup         (1)   snappy             (3)
fermi-lite            (1)   libtasn1        (1)   spaceranger        (1)
ffmpeg                (2)   libtiff         (3)   spades             (2)
ffnvcodec             (2)   libtirpc        (3)   spectra            (1)
fftw.mpi              (2)   libtool         (5)   sqlite             (4)
fftw                  (4)   libunistring    (1)   sra-toolkit        (1)
file                  (2)   libunwind       (3)   ssw                (1)
filevercmp            (1)   libvorbis       (3)   star               (2)
flac                  (3)   libwebp         (1)   stringtie          (1)
flex                  (8)   libxc           (2)   suitesparse        (2)
flexiblas             (4)   libxml2         (6)   swig               (3)
flit                  (1)   libxslt         (2)   szip               (3)
flye                  (1)   libxsmm         (2)   tabixpp            (1)
fontconfig            (3)   libyaml         (2)   tbb                (3)
foss                  (3)   littlecms       (3)   tbl2asn            (2)
freebayes             (1)   llvm            (3)   tcl                (4)
freetype              (3)   lmdb            (3)   tk                 (3)
fribidi               (3)   lpsolve         (2)   tkinter            (3)
fsom                  (1)   lua             (2)   tqdm               (1)
gatk                  (1)   lxml            (1)   trimmomatic        (1)
gc                    (1)   lz4             (3)   trinity            (1)
gcc                   (4)   lzo             (1)   ucc                (3)
gcccore               (4)   m4              (6)   ucx                (5)
gcta                  (1)   maeparser       (2)   udunits            (3)
gdal                  (3)   mafft           (1)   unzip              (4)
gdk-pixbuf            (2)   make            (4)   util-linux         (3)
geos                  (3)   makeinfo        (1)   vcflib             (1)
gettext               (6)   mako            (3)   vcftools           (2)
gfbf                  (2)   mariadb         (1)   vep                (1)
gffcompare            (1)   mash            (1)   virtualenv         (1)
gffread               (1)   matplotlib      (2)   voro++             (2)
ghostscript           (3)   maxquant        (1)   vscode             (1)
giflib                (2)   mdi             (1)   vtk                (1)
git                   (3)   megahit         (2)   wayland            (1)
gitpython             (2)   mesa            (3)   wget               (2)
glib-networking       (1)   meson           (4)   x11                (3)
glib                  (3)   metaeuk         (2)   x264               (2)
glpk                  (3)   metis           (2)   x265               (2)
gmap-gsnap            (1)   miller          (1)   xerces-c++         (1)
gmp                   (3)   miniconda3      (2)   xml-libxml         (2)
gnuplot               (2)   minimap2        (1)   xorg-macros        (4)
gnutls                (1)   mono            (1)   xvfb               (3)
go                    (3)   motif           (1)   xxd                (3)
gobject-introspection (3)   mpfr            (3)   xz                 (4)
gompi                 (4)   mpi4py          (1)   yasm               (2)
googletest            (2)   mrbayes         (2)   z3                 (2)
gperf                 (3)   mrtrix          (1)   zeromq             (2)
graphite2             (2)   multichoose     (1)   zip                (1)
groff                 (3)   multiqc         (2)   zlib               (9)
gromacs               (1)   mummer          (2)   zstd               (3)
gsl                   (3)   nasm            (3)

---------------------- /sw/local/rocky8/epyc3/rcc/modules ----------------------
bolt-lmm (1)   jags        (1)   r-bundle-cran (1)   rjags (1)
eagleimp (1)   lisflood-fp (4)   r             (2)   vasp  (6)

--------------------- /sw/local/rocky8/noarch/rcc/modules ----------------------
alphafold      (3)   diann          (1)   miniforge         (3)
alphapickle    (1)   diffdock       (1)   mobsuite          (1)
amst2          (1)   dynamo         (1)   nnu-net           (1)
ansys          (2)   esa-snap       (1)   orca              (1)
ansysem        (1)   evobind        (1)   perceval-quandela (1)
asreml-sa      (1)   fiji           (3)   proteinmpnn       (1)
asreml-sa_test (1)   fragpipe       (1)   pyem              (1)
aviary         (3)   freesurfer     (1)   qctool            (1)
basespace      (1)   fsl            (1)   qupath            (1)
bindcraft      (2)   gaussian       (1)   r                 (4)
bioformats2raw (1)   gromacs        (4)   relion            (5)
boltz          (3)   gtdb-tk        (3)   rfantibody        (1)
cebraem        (1)   gurobi         (3)   rfdiffusion       (2)
cellsnp-lite   (1)   huygens        (3)   rstudio           (6)
chai-lab       (1)   ilastik        (1)   scenicplus        (1)
chrombpnet     (1)   imod           (2)   schrodinger       (1)
cistem         (1)   itk-snap       (1)   spss              (1)
code-server    (2)   jobstats       (1)   star-ccm+         (2)
compucell3d    (1)   julia          (1)   strainberry       (1)
crested        (1)   localcolabfold (3)   subtom            (1)
crisflash      (1)   mathematica    (1)   tesseract         (1)
cryocare       (1)   matlab         (2)   transcriptm       (1)
cuda-q         (4)   metabolic      (1)   wombat            (1)
deeplabcut     (1)   metaphlan      (1)

--------------------- /sw/local/rocky8/noarch/qcif/modules ---------------------
3d-dna              (1)   isoseq3         (1)   ratatosk        (1)
biobakery_workflows (1)   juicer          (1)   raxml           (1)
blast               (1)   kallisto        (1)   regenie         (1)
braker3             (1)   kofamscan       (1)   repeatmasker    (1)
cellbender          (1)   ldsc            (1)   repeatmodeler   (1)
celseq2             (1)   macs2           (1)   rmats-turbo     (1)
circlator           (1)   maker           (1)   rsem            (1)
dadi                (1)   medaka          (1)   salsa2          (1)
dfam                (1)   mikado          (1)   screen_assembly (1)
diamond             (1)   mira            (1)   scvelo          (1)
dram                (1)   mixer           (1)   shovill         (1)
drep                (1)   mlst            (1)   shpc            (1)
edirect             (1)   mmseqs2         (1)   singlem         (1)
enrichm             (1)   mtag            (1)   snap            (1)
exonerate           (1)   nanocompore     (1)   sortmerna       (1)
f5c                 (1)   nanopolish      (1)   sqanti3         (1)
fastool             (1)   nextpolish      (1)   sra-tools       (1)
gcta                (1)   nextpolish2     (1)   srst2           (1)
gff3sort            (1)   ont-fast5-api   (1)   star            (1)
gmap                (1)   parsnp          (1)   suppa           (1)
gtdbtk              (1)   pb-assembly     (1)   syri            (1)
hapflk              (1)   pear            (1)   transdecoder    (1)
harvesttools        (1)   qapa            (1)   trinity         (1)
hisat2              (1)   qiime2-amplicon (1)   trinotate       (1)
ipyrad              (2)   qiime2-shotgun  (1)   unicycler       (1)
iqtree              (1)   racon           (1)   xpore           (1)
```

## WhatIs List

_TO BE COMPLETED_

## HOW TO GENERATE THESE LISTS

```
module --show-hidden -w 80 -t overview
```
