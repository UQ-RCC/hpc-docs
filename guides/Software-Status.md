# Status of Major Software Installations

## Graphical or Browser Software

Please consult the  [Open OnDemand User Guide](../guides/OnDemand-Guide.md) to see which software is installed and how to run. RStudio, Jupyter Notebooks and Labs, Gaussview, Mathematica and many CVL apps are available through Open OnDemand.

## Licensed Software 

### Mathematica

[**AVAILABLE**]

* Access is restricted to UQ users

* See [Open OnDemand User Guide](../guides/OnDemand-Guide.md)

### SPSS Statistics

* [**AVAILABLE**]

* Access is restrcited to UQ users

See [Open OnDemand User Guide](../guides/OnDemand-Guide.md)


### STATA

* Installation in progress

### Ansys 

[**AVAILABLE**]

* Access is restricted to approved UQ EAIT users only.

* The Ansys dependencies have been built and deployed as a single *mega-module*.
* The issue with the system coupling component now appears to have been resolved following a system configuration patch.
 
To load the dependencies and set the environment for using Ansys:

**`module load ansys/2023.1`**

Please submit a support request via email to rcc-support@uq.edu.au if you experience any issues with Ansys.

___
### Gurobi

[**AVAILABLE**]

* The issue with accessing the Gurobi product license servers on campus has been resolved.
* RCC is working with the vendor and ITS to faciliate access and use of the campus license server.
* Version 9.5.0 has been installed.
* Version 10.0.1 has been installed and configured. 
* Awaiting a patch to the license server to be applied. 
* The licensing patch has been applied.
```
[uq_user@bunya2 ~]$ module purge
[uq_user@bunya2 ~]$ module load gurobi/9.5.0

[uq_user@bunya2 ~]$ alias | grep gurobi
alias check_gurobi_lic='/sw/local/rocky8.6/noarch/rcc/software/Gurobi/gurobi950/linux64/bin/gurobi_cl --license'

[uq_user@bunya2 ~]$ check_gurobi_lic
Set parameter TokenServer to value "uq-gurobi.research.dc.uq.edu.au"
Set parameter LogFile to value "gurobi.log"
Using license file /sw/local/rocky8.6/noarch/rcc/software/Gurobi/gurobi.lic

```

___
### MATLAB 

#### UQ Users

[**AVAILABLE BUT UPDATES BEING TESTED**]

* The version of MATLAB (2022a) that is available does not support some Simulink functionality.
* The Update 6 of R2022a is installed.

Please test the updated version using

**`module load matlab/R2022a6`**

#### Non-UQ 

[**UNAVAILABLE**]

* The access to license servers at home institutions needs to be configured.
* Once that is established, software installation can occur.
___
### Star-CCM+

[**AVAILABLE FOR TESTING**]

* Access to the UQ license server for this product has been established.
* Several dependencies have been deployed.
* Some command line options are essential. Please refer to `module help starccm+/17.02.008`

To test functionality please either of these 

```
module load star-ccm+/15.06.008
module load star-ccm+/17.02.008
```


Please submit a support request via email to rcc-support@uq.edu.au if you experience any issues while testing Star-CCM+.
___
## Full Module List

### CPU Nodes

You should run **`module -I -w 120 --show-hidden overview`** on Bunya to get the up-to-date list of installed software.
```
------------------------------------------ /sw/auto/rocky8c/epyc3/modules/all ------------------------------------------
abricate           (1)   fastp                 (1)   impi            (3)   lz4           (2)   pybigwig        (2)
alsa-lib           (1)   fastqc                (1)   intel-compilers (3)   lzo           (1)   pybind11        (2)
anaconda3          (2)   fasttree              (1)   intel           (3)   m4            (5)   pycoqc          (1)
ansys-dependencies (1)   fermi-lite            (1)   interproscan    (1)   maeparser     (2)   pysam           (2)
ant                (2)   ffmpeg                (1)   intervaltree    (1)   mafft         (1)   python-isal     (2)
any2fasta          (1)   ffnvcodec             (1)   intltool        (2)   make          (3)   python          (7)
archive-zip        (1)   fftw.mpi              (2)   ipython         (2)   makeinfo      (1)   pyyaml          (2)
archspec           (1)   fftw                  (3)   isa-l           (2)   mako          (2)   qhull           (2)
at-spi2-atk        (1)   file                  (2)   jags            (1)   mariadb       (1)   qiime2          (1)
at-spi2-core       (1)   filevercmp            (1)   jansson         (1)   mash          (1)   qt5             (2)
atk                (1)   flac                  (2)   jasper          (2)   matplotlib    (2)   quantumespresso (2)
augustus           (2)   flex                  (7)   java            (1)   maxquant      (1)   quast           (2)
autoconf           (4)   flexiblas             (3)   jbigkit         (2)   megahit       (2)   r               (3)
automake           (4)   flye                  (1)   jellyfish       (2)   mesa          (2)   rapidjson       (2)
autotools          (4)   fontconfig            (2)   jemalloc        (3)   meson         (2)   re2c            (2)
bamtools           (2)   foss                  (3)   jsoncpp         (1)   metaeuk       (2)   rjags           (1)
bbmap              (2)   freebayes             (1)   judy            (1)   metis         (2)   ruby            (2)
bcftools           (2)   freetype              (2)   julia           (1)   miller        (1)   rust            (2)
bcl2fastq2         (1)   fribidi               (2)   jupyter-server  (1)   miniconda3    (2)   salmon          (2)
beagle-lib         (2)   fsom                  (1)   jupyterlab      (1)   minimap2      (1)   samtools        (3)
beagle             (1)   gatk                  (1)   kallisto        (2)   mono          (1)   scafacos        (1)
beautifulsoup      (1)   gc                    (1)   kim-api         (1)   motif         (1)   scalapack       (3)
bedtools           (2)   gcc                   (3)   kraken2         (2)   mpfr          (2)   scikit-build    (1)
binutils           (6)   gcccore               (3)   kronatools      (1)   mrbayes       (2)   scipy-bundle    (2)
bio-db-hts         (1)   gcta                  (1)   lame            (2)   mrtrix        (1)   sdl2            (1)
bio-searchio-hmmer (2)   gdal                  (2)   lammps          (1)   multichoose   (1)   sepp            (2)
bioperl            (2)   gdk-pixbuf            (1)   lapack          (1)   multiqc       (2)   seqlib          (1)
biopython          (2)   geos                  (2)   libaio          (1)   mummer        (2)   seqtk           (2)
bison              (4)   gettext               (4)   libarchive      (3)   nasm          (2)   smithwaterman   (1)
blast+             (2)   gfbf                  (1)   libcerf         (2)   ncbi-vdb      (2)   snakemake       (2)
blast              (1)   gffcompare            (1)   libdeflate      (1)   ncurses       (6)   snappy          (2)
blat               (1)   gffread               (1)   libdrm          (2)   netcdf        (2)   spaceranger     (1)
blis               (3)   ghostscript           (2)   libepoxy        (1)   nettle        (2)   spades          (2)
boost.python       (2)   giflib                (1)   libev           (1)   networkx      (2)   spectra         (1)
boost              (2)   git                   (2)   libevent        (3)   nextflow      (2)   sqlite          (3)
bowtie             (1)   gitpython             (2)   libfabric       (3)   nghttp2       (1)   sra-toolkit     (1)
bowtie2            (2)   glib-networking       (1)   libffi          (3)   nghttp3       (1)   ssw             (1)
brotli             (2)   glib                  (2)   libgd           (2)   ngs           (1)   star            (2)
busco              (2)   glpk                  (2)   libgeotiff      (2)   ngtcp2        (1)   stringtie       (1)
bwa                (2)   gmap-gsnap            (1)   libgit2         (2)   ninja         (2)   suitesparse     (2)
bzip2              (3)   gmp                   (2)   libglu          (4)   nlohmann_json (1)   swig            (2)
c-ares             (1)   gnuplot               (2)   libglvnd        (2)   nlopt         (2)   szip            (2)
cairo              (2)   gnutls                (1)   libiconv        (2)   nodejs        (2)   tabixpp         (1)
canu               (2)   go                    (3)   libidn          (2)   nspr          (2)   tbb             (2)
capnproto          (1)   gobject-introspection (2)   libidn2         (2)   nss           (2)   tbl2asn         (2)
cd-hit             (2)   gompi                 (3)   libint          (2)   numactl       (3)   tcl             (3)
cellranger-arc     (1)   googletest            (1)   libjpeg-turbo   (2)   openbabel     (2)   tk              (2)
cellranger         (1)   gperf                 (2)   libnsl          (1)   openblas      (3)   tkinter         (2)
cereal             (1)   graphite2             (1)   libogg          (2)   openjpeg      (1)   tqdm            (1)
checkm-database    (1)   groff                 (2)   libopus         (1)   openmpi       (3)   trimmomatic     (1)
checkm             (2)   gromacs               (1)   libpciaccess    (3)   openpgm       (2)   trinity         (1)
clang              (3)   gsl                   (2)   libpng          (2)   openssl       (1)   ucc             (2)
cmake              (5)   gtdb-tk               (1)   libpsl          (1)   p11-kit       (1)   ucx             (3)
compress-raw-zlib  (1)   gtk2                  (1)   libreadline     (3)   pandoc        (1)   udunits         (2)
coordgenlibs       (2)   gtk3                  (1)   libsndfile      (2)   pango         (2)   unzip           (3)
cp2k               (2)   guile                 (1)   libsodium       (2)   parallel      (2)   util-linux      (2)
cppy               (2)   gzip                  (2)   libsoup         (1)   pcre          (2)   vcflib          (1)
cunit              (1)   h5py                  (1)   libtasn1        (1)   pcre2         (2)   vcftools        (2)
curl               (3)   harfbuzz              (2)   libtiff         (2)   perl          (5)   vep             (1)
cutadapt           (2)   hdf                   (2)   libtirpc        (2)   picard        (1)   voro++          (1)
db                 (2)   hdf5                  (2)   libtool         (4)   pigz          (2)   wget            (2)
db_file            (2)   help2man              (3)   libunistring    (1)   pillow        (2)   x11             (2)
dbd-mysql          (1)   hifiasm               (1)   libunwind       (2)   pixman        (2)   x264            (1)
dbus               (2)   hipsycl               (1)   libvorbis       (2)   pkg-config    (2)   x265            (1)
deeptools          (2)   hisat2                (2)   libwebp         (1)   pkgconf       (3)   xml-libxml      (2)
dendropy           (2)   hmmer                 (2)   libxc           (2)   pkgconfig     (1)   xorg-macros     (3)
diamond            (2)   htseq                 (1)   libxml2         (5)   plink         (1)   xvfb            (2)
double-conversion  (2)   htslib                (2)   libxslt         (1)   plotly.py     (2)   xxd             (2)
doxygen            (2)   humann                (1)   libxsmm         (2)   plumed        (2)   xz              (3)
easybuild          (2)   hwloc                 (3)   libyaml         (2)   pmix          (3)   yasm            (1)
eigen              (2)   hypothesis            (2)   littlecms       (2)   pocl          (1)   z3              (2)
elfutils           (2)   icu                   (2)   llvm            (2)   popt          (1)   zeromq          (2)
elpa               (2)   iimpi                 (3)   lmdb            (3)   pplacer       (1)   zip             (1)
expat              (2)   imagemagick           (2)   lpsolve         (2)   prodigal      (2)   zlib            (6)
fastahack          (1)   imkl-fftw             (2)   lua             (2)   proj          (2)   zstd            (2)
fastani            (1)   imkl                  (3)   lxml            (1)   prokka        (2)

------------------------------------------ /sw/local/rocky8/epyc3/rcc/modules ------------------------------------------
bolt-lmm (1)   eagleimp (1)   lisflood-fp (3)   vasp (4)

----------------------------------------- /sw/local/rocky8/noarch/rcc/modules ------------------------------------------
ansys     (1)   crisflash (1)   huygens        (2)   mathematica (1)   qctool  (1)   star-ccm+ (2)
asreml-as (1)   gaussian  (1)   ilastik        (1)   matlab      (1)   relion  (3)   wombat    (1)
basespace (1)   gurobi    (2)   localcolabfold (1)   orca        (1)   rstudio (1)

----------------------------------------- /sw/local/rocky8/noarch/qcif/modules -----------------------------------------
3d-dna              (1)   f5c          (1)   macs2         (1)   pear            (1)   shpc         (1)
biobakery_workflows (1)   fastool      (1)   maker         (1)   qapa            (1)   singlem      (1)
blast               (1)   gcta         (1)   medaka        (1)   qiime2-amplicon (1)   snap         (1)
braker3             (1)   gff3sort     (1)   mikado        (1)   qiime2-shotgun  (1)   sortmerna    (1)
cellbender          (1)   gmap         (1)   mira          (1)   racon           (1)   sqanti3      (1)
celseq2             (1)   gtdbtk       (1)   mixer         (1)   ratatosk        (1)   sra-tools    (1)
circlator           (1)   harvesttools (1)   mlst          (1)   raxml           (1)   srst2        (1)
dadi                (1)   hisat2       (1)   mtag          (1)   regenie         (1)   star         (1)
dfam                (1)   ipyrad       (2)   nanocompore   (1)   repeatmasker    (1)   suppa        (1)
diamond             (1)   iqtree       (1)   nanopolish    (1)   repeatmodeler   (1)   transdecoder (1)
dram                (1)   isoseq3      (1)   nextpolish    (1)   rmats-turbo     (1)   trinity      (1)
drep                (1)   juicer       (1)   nextpolish2   (1)   rsem            (1)   trinotate    (1)
edirect             (1)   kallisto     (1)   ont-fast5-api (1)   salsa2          (1)   unicycler    (1)
enrichm             (1)   kofamscan    (1)   parsnp        (1)   scvelo          (1)   xpore        (1)
exonerate           (1)   ldsc         (1)   pb-assembly   (1)   shovill         (1)

```
___
## Software Survey Requests

In late 2022, we asked users to participate in the software survey to ascertain which tools were required on Bunya.
The following table summarises the status of those requests.

|Name|Requests|Responsible|Completed|
|:---|:------:|:--:|:--------|
|Anaconda|96|RCC|YES|
|R|95|RCC|YES|
|GNU compilers (gcc and gfortran)|74|RCC|YES|
|bedtools|56|RCC|YES|
|bamtools|53|RCC|YES|
|fastqc|53|RCC|YES|
|samtools|50|RCC|YES|
|Singularity|49|RCC|YES|
|bcftools|47|RCC|YES|
|OpenMPI (Intel and/or GNU)|46|RCC|YES|
|blast2|45|RCC|YES|
|bowtie2|43|RCC|YES|
|Matlab|41|RCC|YES|
|trimmomatic|36|RCC|YES|
|Intel Compilers (icc and ifort)|29|RCC|YES|
|curl|29|RCC|YES|
|gatk4|27|RCC|YES|
|BLAS|26|RCC|YES|
|IntelMPI|26|RCC|YES|
|gcta|25|RCC|YES|
|LAPACK|24|RCC|YES|
|cutadapt|24|RCC|YES|
|STAR|24|QCIF|YES|
|fastp|23|RCC|YES|
|hisat2|22|QCIF|YES|
|hmmer|22|RCC|YES|
|Julia|20|RCC|YES|
|Gaussian|20|RCC|YES|
|busco|20|RCC|YES|
|picard|20|RCC|YES|
|trinity|20|QCIF/RCC|YES|
|beagle|19|RCC|YES|
|htseq|18|RCC|YES|
|seqtk|18|RCC|YES|
|sra-tools|18|QCIF|YES|
|augustus|17|RCC|YES|
|cellRanger|16|RCC|YES|
|multiQC|16|RCC|YES|
|OpenJDK|15|RCC|YES|
|canu|15|RCC|YES|
|jellyfish|15|RCC|YES|
|RepeatMasker|15|QCIF|YES|
|deeptools|14|RCC|YES|
|Gromacs|13|RCC|YES|
|cd-hit|13|RCC|YES|
|guppy|13|User|YES ... User must install personally licensed copy|
|qiime2|13|RCC|YES|
|transdecoder|13|QCIF|YES|
|Orca|12|RCC||
|LAMMPS|12|RCC|YES|
|gffcompare|12|RCC|YES|
|hclust2|12|QCIF||
|kallisto|12|QCIF|YES|
|pacbio|12|RCC/QCIF||
|snakemake|12|RCC|YES|
|flye|11|RCC|YES|
|interproscan|11|RCC|YES|
|macs2|11|RCC||
|spades|11|RCC |YES|
|trinotate|11|QCIF|YES|
|VASP|10|RCC|YES|
|diamond|10|RCC|YES|
|gmap|10|QCIF||
|prokka|10|RCC|Has been reinstalled due to a dependency issue|
|braker2|9|QCIF|YES but has issues ?|
|checkm|9|RCC|YES|
|htslib|9|RCC|YES|
|kraken2|9|QCIF|YES|
|mafft|9|RCC|YES|
|maker|9|QCIF||
|nextflow|9|RCC|YES|
|quast|9|RCC|YES|
|pb-assembly|8|QCIF||
|repeatmodeler|8|QCIF||
|plink (inc plink 1.9)|8|RCC|YES|
|exonerate|7|QCIF||
|iqtree|7|QCIF||
|VEP|7|RCC||
|ATLAS|6|RCC||
|Nimrod|6|RCC||
|krona|6|RCC|YES|
|mauve|6|RCC||
|NextPolish|6|QCIF||
|SNAP|6|QCIF||
|StarCCM|6|RCC|NEARLY|
|circlator|5|QCIF||
|isoseq3|5|QCIF||
|3d-dna|4|QCIF|YES|
|edirect|4|QCIF||
|raxml|4|RCC||
|cp2k|4|RCC|YES|
|eilmer4|4|User||
|plink2|4|RCC|YES|
|neurodesk|4|User||
|abricate|3|RCC|YES|
|celseq2|3|QCIF||
|dfam|3|QCIF||
|metaphlan|3|QCIF|YES|
|mlst|3|QCIF|YES|
|salsa|3|QCIF|YES|
|spaceRanger|3|QCIF||
|pytorch/tensorflow/cuda|3|RCC||
|gtdb-tk|3|RCC|YES|
|juicer|2|QCIF||
|maxquant|2|RCC |YES|
|mira|2|QCIF||
|pear|2|QCIF||
|cmake|2|RCC|YES|
|ansys|2|RCC|YES|
|gurobi|2|RCC|YES|
|AOCC|1|||
|besst|1|||
|dammit|1|||
|NextDenovo|1|||
|picrust2|1|||
|rcorrector|1|||
|shovill|1|QCIF|YES|
|go (golang)|1|RCC|YES|
|intel mkl|1|RCC|YES|
|parallel|1|RCC|YES|
|vcftools|1|RCC|YES|
|mikado|0|QCIF||
|proovread|0|QCIF||
|ratatosk|0|QCIF||
|sortmerna|0|QCIF||
|humann|0|RCC|YES|
|srst2|0|QCIF||
|rust|0|RCC|YES|
___
## Post Software Survey Requests

These are requests that were not included in the software survey and have been requested since that time. They are necessarily lower priority.

|Name|Requested|Ready?|Note|
|:---|:------:|:--:|:--------|
|DIA-NN|202303|NO|Suitable download found. User is testing|
|Vienna RNA|202303|NO|Installation via EB mechanism yet to be done after initial attempts failed.| 
|Mr Bayes|202303|YES|Installation by modified EB script mechanism successful. Submitting for deployment. Deployed!|
|VBZ Compression Tool||NO||
|FoldX, Rosetta and RFdiffusion||NO||
|LESYMAP|2023-06-01|YES|HackyHour. Identified suitable docker image to use with Apptainer on Bunya.|
|REEF3D||NO|Was installed on Tinaroo previously. User to install with RCC guidance.|

