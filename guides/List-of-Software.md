# List of Additional Software on Bunya

**Updated: 26 August 2026**

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
--------------------- /sw/auto/rocky9a/epyc3/modules/all ----------------------
abricate              (1)    gtk2              (1)   netcdf             (4)
alsa-lib              (1)    gtk3              (2)   nettle             (3)
anaconda3             (2)    guile             (1)   networkx           (3)
ansys-dependencies    (1)    gzip              (4)   nextflow           (3)
ant                   (1)    harfbuzz          (3)   nghttp2            (1)
any2fasta             (1)    hatchling         (3)   nghttp3            (1)
aocl-blas             (1)    hdf               (4)   ngtcp2             (1)
archive-zip           (1)    hdf5              (5)   ninja              (4)
archspec              (2)    help2man          (5)   nlohmann_json      (4)
armadillo             (3)    hifiasm           (1)   nlopt              (2)
arpack-ng             (3)    hisat2            (2)   nodejs             (3)
assimp                (1)    hmmer             (2)   nspr               (3)
at-spi2-atk           (2)    htseq             (1)   nss                (3)
at-spi2-core          (2)    htslib            (3)   numactl            (4)
atk                   (2)    humann            (1)   openbabel          (1)
augustus              (1)    hwloc             (4)   openblas           (4)
autoconf              (5)    hypothesis        (4)   openexr            (3)
automake              (5)    icu               (4)   openfoam           (1)
autotools             (5)    iimpi             (4)   openjpeg           (4)
bamtools              (4)    imagemagick       (2)   openmpi            (4)
bbmap                 (2)    imath             (3)   openpgm            (1)
bcftools              (2)    imkl-fftw         (4)   openssl            (2)
bcl2fastq2            (1)    imkl              (4)   p11-kit            (1)
beagle-lib            (2)    impi              (4)   pandoc             (1)
beagle                (1)    intel-compilers   (4)   pango              (3)
beautifulsoup         (1)    intel             (4)   parallel           (2)
bedtools              (4)    interproscan      (1)   paraview           (1)
binutils              (10)   interproscan_data (1)   patchelf           (3)
bio-db-hts            (1)    intervaltree      (1)   pcre               (4)
bio-searchio-hmmer    (1)    intltool          (3)   pcre2              (4)
bioperl               (2)    ipython           (1)   perl-bundle-cpan   (2)
biopython             (2)    isa-l             (1)   perl               (6)
bison                 (6)    jags              (1)   picard             (1)
blast+                (2)    jansson           (1)   pigz               (1)
blast                 (1)    jasper            (3)   pillow             (2)
blat                  (2)    java              (3)   pixman             (3)
blis                  (4)    jbigkit           (4)   pkg-config         (1)
boost.python          (1)    jellyfish         (2)   pkgconf            (5)
boost                 (4)    jemalloc          (3)   plink              (1)
bowtie                (2)    json-c            (3)   plotly.py          (1)
bowtie2               (2)    json-fortran      (1)   plumed             (3)
brotli                (4)    jsoncpp           (4)   pmix               (4)
brunsli               (3)    judy              (2)   pocl               (1)
build                 (2)    julia             (1)   poetry             (3)
busco                 (1)    jupyter-server    (1)   popt               (1)
bwa                   (2)    jupyterlab        (1)   postgresql         (2)
bzip2                 (4)    kallisto          (2)   pplacer            (1)
c-ares                (1)    kim-api           (2)   prodigal           (2)
cairo                 (3)    kraken2           (1)   proj               (4)
canu                  (1)    kronatools        (1)   prokka             (1)
capnproto             (1)    lame              (3)   prrte              (2)
catch2                (3)    lammps            (2)   psutil             (1)
cd-hit                (1)    lapack            (1)   pybigwig           (1)
cellranger-arc        (1)    lerc              (3)   pybind11           (4)
cellranger            (1)    libaec            (1)   pydantic           (1)
cereal                (2)    libaio            (2)   pysam              (1)
cffi                  (3)    libarchive        (4)   python-bundle-pypi (3)
cfitsio               (3)    libcerf           (1)   python-isal        (1)
cgal                  (1)    libde265          (3)   python             (6)
checkm-database       (1)    libdeflate        (4)   pyyaml             (2)
checkm                (1)    libdrm            (3)   qhull              (5)
clang                 (2)    libepoxy          (2)   qiime2             (1)
cmake                 (6)    libev             (1)   qt5                (2)
compress-raw-zlib     (1)    libevent          (5)   qt6                (1)
coordgenlibs          (1)    libfabric         (4)   quantumespresso    (2)
cp2k                  (1)    libffi            (4)   quast              (1)
cpio                  (2)    libgd             (2)   r-bundle-cran      (2)
cppy                  (2)    libgeotiff        (4)   r                  (4)
cryptography          (3)    libgit2           (2)   rapidjson          (1)
cunit                 (1)    libglu            (4)   re2c               (3)
curl                  (4)    libglvnd          (3)   rjags              (1)
cutadapt              (1)    libheif           (3)   rsem               (1)
cython                (3)    libiconv          (4)   ruby               (1)
db                    (2)    libidn2           (2)   rust               (5)
db_file               (2)    libint            (1)   salmon             (2)
dbd-mysql             (1)    libjpeg-turbo     (4)   samtools           (3)
dbus                  (3)    libnsl            (1)   scafacos           (2)
deeptools             (1)    libogg            (2)   scalapack          (4)
dendropy              (2)    libopus           (2)   scikit-build-core  (1)
dftd4                 (1)    libpciaccess      (4)   scikit-build       (3)
diamond               (1)    libpng            (4)   scipy-bundle       (4)
dirac                 (1)    libpsl            (2)   scotch             (1)
double-conversion     (3)    libreadline       (4)   sdl2               (3)
doxygen               (4)    libsndfile        (2)   sepp               (2)
easybuild             (1)    libsodium         (1)   seqlib             (1)
eigen                 (4)    libsoup           (1)   seqtk              (4)
elfutils              (1)    libtasn1          (1)   setuptools-rust    (3)
elpa                  (2)    libtiff           (4)   skani              (1)
expat                 (4)    libtirpc          (4)   smithwaterman      (1)
fastahack             (1)    libtool           (5)   snakemake          (1)
fastp                 (1)    libunistring      (2)   snappy             (3)
fastqc                (1)    libunwind         (3)   spaceranger        (2)
fasttree              (1)    libvorbis         (2)   spades             (1)
fermi-lite            (1)    libvori           (1)   spectra            (1)
ffmpeg                (3)    libwebp           (3)   spin               (1)
ffnvcodec             (3)    libxc             (2)   sqlite             (4)
fftw.mpi              (4)    libxml2           (6)   sra-toolkit        (2)
fftw                  (4)    libxslt           (3)   ssw                (1)
file                  (2)    libxsmm           (1)   star               (2)
filevercmp            (1)    libyaml           (2)   stringtie          (1)
flac                  (2)    lit               (3)   suitesparse        (1)
flex                  (8)    littlecms         (2)   swig               (4)
flexiblas             (4)    llvm              (3)   szip               (4)
flit                  (3)    lmdb              (3)   tabixpp            (1)
flye                  (1)    lpsolve           (2)   tbb                (3)
fontconfig            (3)    lua               (1)   tbl2asn            (1)
fonttools             (1)    lxml              (1)   tcl                (4)
foss                  (4)    lz4               (4)   tk                 (3)
freebayes             (1)    lzo               (2)   tkinter            (2)
freetype              (3)    m4                (8)   tmux               (1)
fribidi               (3)    maeparser         (1)   tqdm               (1)
fsom                  (1)    mafft             (1)   trimmomatic        (1)
gatk                  (2)    make              (4)   trinity            (1)
gc                    (1)    makeinfo          (2)   typing-extensions  (1)
gcc                   (5)    mako              (3)   ucc                (4)
gcccore               (5)    mariadb           (2)   ucx                (4)
gcta                  (1)    mash              (1)   udunits            (2)
gdal                  (3)    matplotlib        (2)   unzip              (4)
gdk-pixbuf            (3)    maturin           (2)   util-linux         (3)
geos                  (4)    maxquant          (1)   vcflib             (1)
gettext               (7)    mctc-lib          (1)   vcftools           (2)
gfbf                  (4)    mdi               (2)   vep                (1)
gffcompare            (1)    megahit           (1)   virtualenv         (3)
gffread               (1)    mesa              (3)   voro++             (2)
ghostscript           (2)    meson-python      (3)   vscode             (1)
giflib                (4)    meson             (4)   vtk                (2)
git                   (4)    metaeuk           (2)   wayland            (2)
gitpython             (1)    metis             (1)   wfa2               (1)
glib-networking       (1)    miller            (1)   wget               (1)
glib                  (3)    miniconda3        (2)   x11                (3)
glpk                  (2)    minimap2          (1)   x264               (3)
gmap-gsnap            (2)    miniprot          (1)   x265               (3)
gmp                   (3)    mono              (1)   xerces-c++         (3)
gnuplot               (1)    motif             (1)   xml-libxml         (2)
gnutls                (1)    mpfr              (3)   xorg-macros        (4)
go                    (4)    mpi4py            (3)   xtb                (1)
gobject-introspection (3)    mrbayes           (2)   xvfb               (2)
gompi                 (8)    mstore            (1)   xxd                (3)
googletest            (4)    multicharge       (1)   xz                 (4)
gperf                 (3)    multichoose       (1)   yasm               (3)
graphite2             (3)    multiqc           (1)   z3                 (2)
groff                 (3)    mummer            (1)   zeromq             (1)
gromacs               (3)    nasm              (4)   zip                (1)
gsl                   (3)    ncbi-vdb          (2)   zlib               (9)
gtdb-tk               (1)    ncurses           (7)   zstd               (4)

--------------------- /sw/local/rocky8/epyc3/rcc/modules ----------------------
bolt-lmm (1)   hdf5   (1)   lisflood-fp   (4)   rjags (1)
dirac    (1)   jags   (1)   r-bundle-cran (1)   vasp  (6)
eagleimp (1)   libaec (1)   r             (2)

--------------------- /sw/local/rocky8/noarch/rcc/modules ---------------------
alphafast      (1)   epi2me         (1)   openfold          (3)
alphafold      (4)   esa-snap       (1)   orca              (1)
alphapickle    (1)   evobind        (1)   osca              (1)
amst2          (1)   fastfold       (1)   paraview          (1)
ansys          (3)   fbpic          (1)   perceval-quandela (1)
ansysem        (1)   fiji           (3)   porechop_abi      (1)
asreml-sa      (3)   fragpipe       (1)   post              (1)
asreml-sa_test (1)   freesurfer     (1)   prism             (1)
aviary         (4)   fsl            (1)   proteina-complexa (1)
bagel          (1)   gaussian       (1)   proteinfold       (1)
bakta          (1)   gromacs        (4)   proteinmpnn       (1)
basespace      (1)   gtdb-tk        (3)   pyem              (1)
binchicken     (1)   gurobi         (4)   qctool            (1)
bindcraft      (3)   humann         (1)   quilt             (1)
bioformats2raw (1)   huygens        (4)   qupath            (3)
boltz          (3)   ilastik        (2)   r                 (6)
boltzgen       (1)   imod           (2)   relion            (9)
carpdock       (1)   interproscan   (1)   remora            (2)
cebraem        (1)   ipyrad         (1)   rfantibody        (1)
cellpose       (2)   itk-snap       (1)   rfdiffusion       (2)
cellprofiler   (1)   jobstats       (1)   rosetta           (1)
cellsnp-lite   (1)   julia          (1)   rstudio           (9)
chai-lab       (2)   ligandmpnn     (1)   scenicplus        (1)
chimerax       (1)   llama.cpp      (3)   schrodinger       (1)
chrombpnet     (1)   localcolabfold (3)   sglang            (1)
cistem         (1)   mathematica    (1)   slorado           (2)
code-server    (4)   matlab         (3)   spisonet          (1)
compucell3d    (1)   medaka         (3)   spss              (1)
coot           (2)   metabolic      (1)   star-ccm+         (3)
cramino        (1)   metaphlan      (2)   strainberry       (1)
crested        (2)   miniforge      (4)   subtom            (1)
crisflash      (1)   minimap2       (1)   suite2p           (2)
cryocare       (1)   mmseqs         (2)   tesseract         (1)
cryodrgn       (2)   mobsuite       (1)   topaz             (1)
cuda-q         (4)   model-angelo   (1)   transcriptm       (1)
deeplabcut     (5)   mrtrix         (1)   triqs             (1)
diann          (2)   nastic         (1)   ultralytics       (1)
diffdock       (1)   nnu-net        (1)   virtualgl         (2)
dl-jupyter     (2)   ollama         (1)   vllm              (5)
dorado         (1)   openclip       (2)   wombat            (1)
dynamo         (1)   openfoam       (1)   xds               (1)

--------------------- /sw/local/rocky9/noarch/rcc/modules ---------------------
ansys         (5)   deeptmhmm     (1)   huygens    (2)   pclai     (1)
autodock-gpu  (1)   diamond       (1)   lastools   (1)   proteinix (1)
autodock-vina (1)   eggnog-mapper (1)   lexicmap   (1)   space     (1)
clustal-omega (1)   evo2          (1)   macs2      (1)   star-ccm+ (1)
coverm        (1)   group_envs    (1)   nanomotif  (1)   vasp      (1)
crest         (1)   gtdb-tk       (1)   parabricks (1)

-------------------- /sw/local/rocky8/noarch/qcif/modules ---------------------
3d-dna              (1)   isoseq3         (1)   raxml           (1)
biobakery_workflows (1)   juicer          (1)   regenie         (1)
blast               (1)   kallisto        (1)   repeatmasker    (1)
braker3             (1)   kofamscan       (1)   repeatmodeler   (1)
cellbender          (1)   ldsc            (1)   rmats-turbo     (1)
celseq2             (1)   maker           (1)   rsem            (1)
circlator           (1)   medaka          (1)   salsa2          (1)
dadi                (1)   mikado          (1)   screen_assembly (1)
dfam                (1)   mira            (1)   scvelo          (1)
diamond             (1)   mixer           (1)   shovill         (1)
dram                (1)   mlst            (1)   shpc            (1)
drep                (1)   mmseqs2         (1)   singlem         (1)
edirect             (1)   mtag            (1)   snap            (1)
enrichm             (1)   nanocompore     (1)   sortmerna       (1)
exonerate           (1)   nanopolish      (1)   sqanti3         (1)
f5c                 (1)   nextpolish      (1)   sra-tools       (1)
fastool             (1)   nextpolish2     (1)   srst2           (1)
gcta                (1)   ont-fast5-api   (1)   star            (1)
gff3sort            (1)   parsnp          (1)   suppa           (1)
gmap                (1)   pb-assembly     (1)   syri            (1)
gtdbtk              (1)   pear            (1)   transdecoder    (1)
hapflk              (1)   qapa            (1)   trinity         (1)
harvesttools        (1)   qiime2-amplicon (1)   trinotate       (1)
hisat2              (1)   qiime2-shotgun  (1)   unicycler       (1)
ipyrad              (2)   racon           (1)   xpore           (1)
iqtree              (1)   ratatosk        (1)


```

## The Module WhatIs List

_TO BE COMPLETED_

## onBunya Applications

|Application|Category 1|Category 2|
|:---|:---:|:---:|
|3dslicer (4.10.1)|General-Imaging|Neuroimaging|
|3dslicer (5.12.0)|General-imaging|Neuroimaging|
|3dslicer (5.12.3)|General-imaging|Neuroimaging|
|3dslicer (5.8.1)|General-imaging|Neuroimaging|
|Adxv|Crystallography|General-scientific|
|AFNI|Imaging|Neuroimaging|
|AlphaFold 2.3.2|AI-ML|Struct-bio|
|ANTs|Misc|General-imaging|
|BIDScoin|Imaging|Neuroimaging|
|Blender|Misc|General-imaging|
|Cellpose 3.1.0|Misc|Struct-bio|
|Cellpose-SAM|Misc|Struct-bio|
|Cellprofiler 4.2.1|Misc|Cytometry|
|Cellprofiler 4.2.8.1|Misc|Cytometry|
|ChimeraX 1.12|Misc|Cryo-EM|
|CisTEM 2|CryoEM|Cryo-EM|
|CisTEM|CryoEM|Cryo-EM|
|ComfyUI|AI-ML||
|CompuCell3D|Misc|Struct-bio|
|Coot 0.9.8.92|Misc|Struct-bio|
|Cryolo|Misc|Struct-bio|
|CryoSPARC|CryoEM|Struct-bio|
|CryoSPARC updater (to 5.0.4)|CryoEM|Struct-bio|
|Crystfel|CryoEM|Cryo-EM|
|Cytoscape|Bioinformatics|Cytometry|
|DeepLabCut 2.3.11 (AMD GPU)|AI-ML|Struct-bio|
|DeepLabCut 2.3.8 (NVidia GPU)|AI-ML|Struct-bio|
|DeepLabCut 3.0.0rc10 (AMD GPU)|AI-ML|Struct-bio|
|DeepLabCut 3.0.0rc10 (NVidia GPU)|AI-ML|Struct-bio|
|DIA-NN|Bioinformatics||
|Diffusion Toolkit|Imaging|Neuroimaging|
|Dynamo 1.1.532|Misc|General-scientific|
|EMAN 2.3|CryoEM|Struct-bio|
|Empanada (Napari)|General-imaging|Cryo-EM|
|EPI2ME|Bioinformatics||
|ESA SNAP 10.0.0|Misc|General-scientific|
|ESA SNAP 9.0|Misc|General-scientific|
|Eye of MATE Image Viewer|Misc|General-imaging|
|Fiji 1.53|Fiji||
|Fiji 1.54h|Fiji||
|Fiji 1.54h (No Cellpose)|Fiji||
|Fiji 1.54k|Fiji||
|Fiji 1.54k (No Cellpose)|Fiji||
|Fiji 1.54p|Fiji||
|Fiji 1.54q|Fiji||
|Fiji 1.54t|Fiji||
|FoldDock|AI-ML|Struct-bio|
|FragPipe|Struct-bio||
|Freesurfer 7.3.2|Imaging|Neuroimaging|
|FSL 5.0|Imaging|Neuroimaging|
|FSL 6.0.7.9|Imaging|Neuroimaging|
|HRM Online - Huygens Core|Scientific|Volume|
|Huygens Essential|Scientific|Volume|
|Huygens Localizer|Scientific|Volume|
|Huygens Professional|Scientific|Volume|
|IGV|Bioinformatics||
|Ilastik 1.4.1|Misc|Cytometry|
|IMOD 4.11.4|Misc|General-imaging|
|IMOD 4.12.62|Misc|General-imaging|
|IMOD 4.9.9|Misc|General-imaging|
|IMOD 5.1.1|Misc|General-imaging|
|IMOD-RAZA|Misc|General-imaging|
|ITK-SNAP (4.2.0)|Misc|General-imaging|
|ITK-SNAP (4.4.0)|Misc|General-imaging|
|Jupyter notebook|Misc|General-scientific|
|LabGym 2.8.1|AI-ML||
|LiberTEM|Misc|Cryo-EM|
|LibreOffice|Misc|General-scientific|
|LLAma.cpp|AI-ML||
|Mathematica 14.0|Misc|General-scientific|
|Matlab 2022a6|Misc|General-scientific|
|Matlab 2023b5|Misc|General-scientific|
|Matlab MCR (v93, for R2017b)|Misc|General-scientific|
|Matlab MCR (v97, for R2019b)|Misc|General-scientific|
|MIB|Crystallography|Struct-bio|
|Minc Tools|Imaging|Neuroimaging|
|Model-angelo|CryoEM|Cryo-EM|
|MolSketch|Misc|General-imaging|
|MrTrix 3.0.8|Imaging|Neuroimaging|
|MrTrix 3|Imaging|Neuroimaging|
|MrTrix|Imaging|Neuroimaging|
|Napari (0.4.10)|Misc|General-imaging|
|Napari (0.5.3)|Misc|General-imaging|
|Napari (0.6.2)|Misc|General-imaging|
|NoiseTransfer2Clean|CryoEM|Struct-bio|
|Octave 9.2.0|Misc|General-scientific|
|Olex2|Crystallography|Struct-bio|
|OMERO.insight|Misc|Light-microscopy|
|Open WebUI|AI-ML||
|Paraview|Misc|General-imaging|
|Phenix 1.20.1|Crystallography|Struct-bio|
|Phenix 1.21.1|Crystallography|Struct-bio|
|Phenix 2.1 (no GPU)|Crystallography|Struct-bio|
|Phenix 2.1 (NVidia GPU)|Crystallography|Struct-bio|
|PyEM|Misc|Cryo-EM|
|PyMOL|Misc|General-imaging|
|QGIS|Misc|General-imaging|
|QuPath 0.7.0|Cytometry|General-imaging|
|Relion 4.0|CryoEM|Struct-bio|
|Relion 5.0.1|CryoEM|Struct-bio|
|Rstudio 2024.04.2 (R 4.4.1)|Misc|General-scientific|
|Rstudio 2024.12.0 (R 4.4.2, 25k pkgs)|Rstudio||
|Rstudio 2024.12.1 (R 4.4.2, 1200 pkgs)|Rstudio||
|Rstudio 2025.05.1 (R 4.5.1)|Rstudio||
|Rstudio 2026.01.0 (R 4.5.2)|Rstudio||
|Rstudio 2026.07.0 (R 4.6.1)|Rstudio||
|Schrodinger Maestro|Misc|Struct-bio|
|ScigetApp|Misc|General-scientific|
|Scipion3|Misc|Struct-bio|
|Scipion3 (with Relion)|Misc|Struct-bio|
|Scipion3 (with XmippSrc)|Misc|Struct-bio|
|SHELX|Crystallography|Struct-bio|
|ShelXle|Crystallography|Struct-bio|
|Sir2019|CryoEM|Cryo-EM|
|SPHIRE 1.4|CryoEM|Struct-bio|
|SPM 12|Imaging|CVL|
|Spyder|Misc|General-scientific|
|StaMPS|Misc|General-scientific|
|Suite2p|Misc|General-imaging|
|THUNDER|CryoEM|Cryo-EM|
|TomoBear 0.6.0|CryoEM|Struct-bio|
|Topaz|CryoEM|Cryo-EM|
|TrackVis|Imaging|Neuroimaging|
|TrackVis shell|Imaging|Neuroimaging|
|VESTA|Crystallography|Struct-bio|
|VLC Media Player|Misc|General-imaging|
|VMD 2.0.1a1|Misc|General-imaging|
|VMD|Misc|General-imaging|
|XDS 2021|Crystallography|Struct-bio|
|XDS 2025|Crystallography|Struct-bio|




## HOW TO GENERATE THESE LISTS

```
#Module Overview List
module --show-hidden -w 80 -t overview

#onBunya List
/sw/admin/davidg/bin/createOnBunyaAppsList 

```
