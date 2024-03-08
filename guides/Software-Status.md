# Status of Major Software Installations

## Licensed Software 

### Mathematica

* Installation in progress

### SPSS

* Installation in progress

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

----------------------------------------- /sw/auto/rocky8.6/epyc3/modules/all ------------------------------------------
abricate           (1)   fermi-lite            (1)   interproscan  (1)   makeinfo        (2)   pyyaml            (2)
alsa-lib           (1)   ffmpeg                (2)   intervaltree  (1)   mako            (2)   qhull             (2)
anaconda3          (1)   fftw.mpi              (1)   intltool      (2)   mash            (1)   qiime2            (1)
ansys-dependencies (1)   fftw                  (4)   ipython       (1)   matplotlib      (2)   quantumespresso   (1)
ant                (1)   file                  (1)   isa-l         (2)   maxquant        (1)   quast             (1)
any2fasta          (1)   filevercmp            (1)   jags          (1)   megahit         (1)   r                 (2)
aocc               (1)   flac                  (1)   jansson       (1)   mesa            (2)   rapidjson         (2)
archspec           (1)   flex                  (6)   jasper        (1)   meson           (2)   re2c              (1)
at-spi2-atk        (1)   flexiblas             (2)   java          (1)   metaeuk         (1)   rjags             (1)
at-spi2-core       (1)   flye                  (1)   jbigkit       (2)   metis           (1)   ruby              (2)
atk                (1)   fontconfig            (2)   jellyfish     (1)   miller          (1)   rust              (2)
augustus           (1)   foss                  (4)   jemalloc      (2)   miniconda3      (1)   salmon            (1)
autoconf           (4)   freebayes             (1)   jsoncpp       (1)   mono            (1)   samtools          (1)
automake           (4)   freetype              (2)   julia         (1)   motif           (1)   scafacos          (1)
autotools          (4)   fribidi               (2)   kallisto      (1)   mpfr            (2)   scalapack         (4)
bamtools           (1)   fsom                  (1)   kim-api       (1)   mrbayes         (1)   scikit-build      (1)
bbmap              (1)   gatk                  (1)   kraken2       (1)   multichoose     (1)   scipy-bundle      (2)
bcftools           (2)   gaussian              (1)   kronatools    (1)   multiqc         (1)   sdl2              (1)
beagle-lib         (1)   gc                    (1)   lame          (2)   nasm            (2)   sepp              (1)
beagle             (1)   gcc                   (4)   lammps        (1)   ncbi-vdb        (1)   seqlib            (1)
bedtools           (1)   gcccore               (4)   lapack        (1)   nccl            (2)   seqtk             (1)
binutils           (8)   gcta                  (1)   libarchive    (2)   ncurses         (6)   smithwaterman     (1)
bio-searchio-hmmer (1)   gdal                  (1)   libcerf       (1)   netcdf          (1)   snakemake         (1)
bioperl            (1)   gdk-pixbuf            (1)   libdeflate    (1)   nettle          (2)   snappy            (1)
biopython          (1)   gdrcopy               (2)   libdrm        (2)   networkx        (1)   spades            (1)
bison              (6)   geos                  (1)   libepoxy      (1)   nextflow        (1)   spectra           (1)
blast+             (1)   gettext               (5)   libev         (1)   nghttp2         (1)   sqlite            (2)
blast              (1)   gfbf                  (1)   libevent      (3)   nghttp3         (1)   ssw               (1)
blis               (2)   gffcompare            (1)   libfabric     (3)   ngs             (1)   star              (1)
boost              (2)   gffread               (1)   libffi        (2)   ngtcp2          (1)   stringtie         (1)
bowtie2            (2)   ghostscript           (1)   libgd         (1)   ninja           (2)   suitesparse       (1)
brotli             (2)   giflib                (1)   libgeotiff    (1)   nlopt           (1)   swig              (2)
busco              (1)   git                   (2)   libgit2       (1)   nodejs          (1)   szip              (1)
bwa                (1)   gitpython             (1)   libglu        (3)   nspr            (1)   tabixpp           (1)
bzip2              (2)   glib-networking       (1)   libglvnd      (2)   nss             (1)   tbb               (2)
c-ares             (1)   glib                  (2)   libiconv      (1)   numactl         (4)   tbl2asn           (2)
cairo              (2)   glpk                  (1)   libidn        (2)   openblas        (4)   tcl               (2)
capnproto          (1)   gmp                   (2)   libidn2       (2)   openmpi         (4)   tk                (2)
cd-hit             (1)   gnutls                (1)   libint        (1)   openpgm         (1)   tkinter           (2)
cellranger         (1)   go                    (2)   libjpeg-turbo (2)   openssl         (1)   tqdm              (1)
checkm             (1)   gobject-introspection (2)   libnsl        (1)   p11-kit         (1)   trimmomatic       (1)
clang              (1)   gompi                 (4)   libogg        (1)   pango           (2)   trinity           (1)
cmake              (2)   gperf                 (2)   libpciaccess  (4)   parallel        (1)   typing-extensions (1)
coordgenlibs       (2)   groff                 (3)   libpng        (2)   pcre            (2)   ucc               (1)
cp2k               (1)   gromacs               (1)   libpsl        (1)   pcre2           (1)   ucx-cuda          (2)
cppy               (2)   gsl                   (2)   libreadline   (3)   perl            (6)   ucx               (3)
cuda               (4)   gtdb-tk               (2)   libsndfile    (1)   picard          (1)   udunits           (1)
cudnn              (4)   gtk2                  (1)   libsodium     (1)   pigz            (1)   unzip             (2)
cunit              (1)   gtk3                  (1)   libsoup       (1)   pillow          (2)   util-linux        (2)
curl               (2)   guile                 (1)   libtasn1      (1)   pixman          (2)   vasp              (1)
cutadapt           (1)   gzip                  (2)   libtiff       (2)   pkg-config      (3)   vcflib            (1)
cutensor           (1)   h5py                  (1)   libtirpc      (2)   pkgconf         (2)   vcftools          (1)
db                 (4)   harfbuzz              (2)   libtool       (4)   pkgconfig       (1)   voro++            (1)
db_file            (1)   hdf                   (1)   libunistring  (1)   plink           (1)   wget              (1)
dbus               (2)   hdf5                  (1)   libunwind     (2)   plotly.py       (1)   x11               (2)
deeptools          (1)   help2man              (4)   libvorbis     (1)   plumed          (1)   x264              (2)
dendropy           (1)   hifiasm               (1)   libwebp       (1)   pmix            (4)   x265              (2)
diamond            (1)   hisat2                (1)   libxc         (1)   pocl            (1)   xml-libxml        (1)
double-conversion  (1)   hmmer                 (1)   libxml2       (5)   popt            (1)   xorg-macros       (4)
doxygen            (1)   htseq                 (1)   libxslt       (1)   pplacer         (1)   xvfb              (1)
easybuild          (2)   htslib                (2)   libxsmm       (1)   prodigal        (1)   xxd               (1)
eigen              (2)   humann                (1)   libyaml       (2)   proj            (1)   xz                (4)
elfutils           (1)   hwloc                 (4)   littlecms     (1)   prokka          (1)   yasm              (2)
elpa               (1)   hypothesis            (2)   llvm          (2)   protobuf-python (2)   z3                (1)
expat              (4)   icu                   (2)   lmdb          (2)   protobuf        (2)   zeromq            (1)
expecttest         (2)   iimpi                 (1)   lpsolve       (1)   pybigwig        (1)   zlib              (6)
fastahack          (1)   imagemagick           (1)   lz4           (2)   pybind11        (2)   zstd              (2)
fastani            (1)   imkl                  (2)   m4            (6)   pycoqc          (1)
fastp              (1)   impi                  (1)   maeparser     (2)   pysam           (2)
fastqc             (1)   intel-compilers       (1)   mafft         (1)   python-isal     (1)
fasttree           (1)   intel                 (1)   magma         (2)   python          (6)

----------------------------------------- /sw/local/rocky8.6/epyc3/rcc/modules -----------------------------------------
matlab (1)

---------------------------------------- /sw/local/rocky8.6/noarch/rcc/modules -----------------------------------------
ansys (1)   gurobi (2)   matlab (1)   star-ccm+ (2)

---------------------------------------- /sw/local/rocky8.6/epyc3/qcif/modules -----------------------------------------
3d-dna              (1)   braker3 (1)   gtdbtk (1)   rmats-turbo (1)   shovill (1)
biobakery_workflows (1)   enrichm (1)   mtag   (1)   salsa2      (1)   shpc    (1)

---------------------------------------- /sw/local/rocky8.6/noarch/qcif/modules ----------------------------------------
blast    (1)   hisat2    (1)   mixer       (1)   ont-fast5-api (1)   sra-tools    (1)   trinotate (1)
f5c      (1)   kallisto  (1)   mlst        (1)   repeatmasker  (1)   star         (1)   xpore     (1)
fastool  (1)   kofamscan (1)   nanocompore (1)   repeatmodeler (1)   transdecoder (1)
gff3sort (1)   ldsc      (1)   nanopolish  (1)   rsem          (1)   trinity      (1)


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

