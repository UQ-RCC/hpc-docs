# Status of Major Software Installations

## Licensed Software 

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

To test functionality please 

**`module load star-ccm+/.17.02.008`**

Please submit a support request via email to rcc-support@uq.edu.au if you experience any issues while testing Star-CCM+.
___
## Full Module List

You should run **`module -I -w 120 --show-hidden overview`** on Bunya to get the up-to-date list of installed software.
```

----------------------------------------- /sw/auto/rocky8.6/epyc3/modules/all ------------------------------------------
abricate           (1)   ffmpeg                (2)   interproscan  (1)   mafft           (1)   pyyaml            (2)
alsa-lib           (1)   fftw.mpi              (1)   intervaltree  (1)   magma           (2)   qhull             (2)
anaconda3          (1)   fftw                  (4)   intltool      (2)   makeinfo        (2)   qiime2            (1)
ansys-dependencies (1)   filevercmp            (1)   ipython       (1)   mako            (2)   quantumespresso   (1)
ant                (1)   flac                  (1)   isa-l         (2)   mash            (1)   quast             (1)
any2fasta          (1)   flex                  (6)   jags          (1)   matplotlib      (2)   r                 (2)
aocc               (1)   flexiblas             (2)   jansson       (1)   maxquant        (1)   re2c              (1)
archspec           (1)   flye                  (1)   jasper        (1)   megahit         (1)   rjags             (1)
at-spi2-atk        (1)   fontconfig            (2)   java          (1)   mesa            (2)   ruby              (2)
at-spi2-core       (1)   foss                  (4)   jbigkit       (2)   meson           (2)   rust              (2)
atk                (1)   freebayes             (1)   jellyfish     (1)   metaeuk         (1)   salmon            (1)
augustus           (1)   freetype              (2)   jemalloc      (2)   metis           (1)   samtools          (1)
autoconf           (4)   fribidi               (2)   jsoncpp       (1)   miller          (1)   scafacos          (1)
automake           (4)   fsom                  (1)   julia         (1)   miniconda3      (1)   scalapack         (4)
autotools          (4)   gatk                  (1)   kallisto      (1)   mono            (1)   scikit-build      (1)
bamtools           (1)   gaussian              (1)   kim-api       (1)   motif           (1)   scipy-bundle      (2)
bbmap              (1)   gc                    (1)   kraken2       (1)   mpfr            (2)   sdl2              (1)
bcftools           (2)   gcc                   (4)   kronatools    (1)   multichoose     (1)   sepp              (1)
beagle             (1)   gcccore               (4)   lame          (2)   multiqc         (1)   seqlib            (1)
bedtools           (1)   gcta                  (1)   lammps        (1)   nasm            (2)   seqtk             (1)
binutils           (8)   gdal                  (1)   lapack        (1)   nccl            (2)   smithwaterman     (1)
bio-searchio-hmmer (1)   gdk-pixbuf            (1)   libarchive    (2)   ncurses         (6)   snakemake         (1)
bioperl            (1)   gdrcopy               (2)   libcerf       (1)   netcdf          (1)   snappy            (1)
biopython          (1)   geos                  (1)   libdeflate    (1)   nettle          (2)   spades            (1)
bison              (6)   gettext               (5)   libdrm        (2)   networkx        (1)   spectra           (1)
blast+             (1)   gfbf                  (1)   libepoxy      (1)   nextflow        (1)   sqlite            (2)
blast              (1)   gffcompare            (1)   libev         (1)   nghttp2         (1)   ssw               (1)
blis               (2)   gffread               (1)   libevent      (3)   nghttp3         (1)   star              (1)
boost              (2)   ghostscript           (1)   libfabric     (3)   ngtcp2          (1)   stringtie         (1)
bowtie2            (2)   giflib                (1)   libffi        (2)   ninja           (2)   suitesparse       (1)
brotli             (2)   git                   (2)   libgd         (1)   nlopt           (1)   swig              (2)
busco              (1)   gitpython             (1)   libgeotiff    (1)   nodejs          (1)   szip              (1)
bwa                (1)   glib-networking       (1)   libgit2       (1)   nspr            (1)   tabixpp           (1)
bzip2              (2)   glib                  (2)   libglu        (3)   nss             (1)   tbb               (2)
c-ares             (1)   glpk                  (1)   libglvnd      (2)   numactl         (4)   tbl2asn           (1)
cairo              (2)   gmp                   (2)   libiconv      (1)   openblas        (4)   tcl               (2)
capnproto          (1)   gnutls                (1)   libidn        (1)   openmpi         (4)   tk                (2)
cd-hit             (1)   go                    (2)   libidn2       (2)   openpgm         (1)   tkinter           (2)
cellranger         (1)   gobject-introspection (2)   libint        (1)   openssl         (1)   tqdm              (1)
checkm             (1)   gompi                 (4)   libjpeg-turbo (2)   p11-kit         (1)   trimmomatic       (1)
cmake              (2)   gperf                 (2)   libnsl        (1)   pango           (2)   trinity           (1)
cp2k               (1)   groff                 (3)   libogg        (1)   parallel        (1)   typing-extensions (1)
cppy               (2)   gromacs               (1)   libpciaccess  (4)   pcre            (2)   ucc               (1)
cuda               (4)   gsl                   (2)   libpng        (2)   pcre2           (1)   ucx-cuda          (2)
cudnn              (4)   gtdb-tk               (2)   libpsl        (1)   perl            (6)   ucx               (3)
cunit              (1)   gtk2                  (1)   libreadline   (3)   picard          (1)   udunits           (1)
curl               (2)   gtk3                  (1)   libsndfile    (1)   pigz            (1)   unzip             (2)
cutadapt           (1)   guile                 (1)   libsodium     (1)   pillow          (2)   util-linux        (2)
cutensor           (1)   gzip                  (2)   libsoup       (1)   pixman          (2)   vasp              (1)
db                 (4)   h5py                  (1)   libtasn1      (1)   pkg-config      (3)   vcflib            (1)
db_file            (1)   harfbuzz              (2)   libtiff       (2)   pkgconf         (2)   vcftools          (1)
dbus               (2)   hdf                   (1)   libtirpc      (2)   pkgconfig       (1)   voro++            (1)
deeptools          (1)   hdf5                  (1)   libtool       (4)   plink           (1)   wget              (1)
dendropy           (1)   help2man              (4)   libunistring  (1)   plotly.py       (1)   x11               (2)
diamond            (1)   hifiasm               (1)   libunwind     (2)   plumed          (1)   x264              (2)
double-conversion  (1)   hmmer                 (1)   libvorbis     (1)   pmix            (4)   x265              (2)
doxygen            (1)   htseq                 (1)   libwebp       (1)   popt            (1)   xml-libxml        (1)
easybuild          (2)   htslib                (2)   libxc         (1)   pplacer         (1)   xorg-macros       (4)
eigen              (2)   humann                (1)   libxml2       (5)   prodigal        (1)   xvfb              (1)
elpa               (1)   hwloc                 (4)   libxslt       (1)   proj            (1)   xxd               (1)
expat              (4)   hypothesis            (2)   libxsmm       (1)   protobuf-python (2)   xz                (4)
expecttest         (2)   icu                   (2)   libyaml       (2)   protobuf        (2)   yasm              (2)
fastahack          (1)   iimpi                 (1)   littlecms     (1)   pybigwig        (1)   zeromq            (1)
fastani            (1)   imagemagick           (1)   llvm          (2)   pybind11        (2)   zlib              (6)
fastp              (1)   imkl                  (2)   lmdb          (2)   pycoqc          (1)   zstd              (2)
fastqc             (1)   impi                  (1)   lpsolve       (1)   pysam           (2)
fasttree           (1)   intel-compilers       (1)   lz4           (2)   python-isal     (1)
fermi-lite         (1)   intel                 (1)   m4            (6)   python          (5)

----------------------------------------- /sw/local/rocky8.6/epyc3/rcc/modules -----------------------------------------
matlab (1)

---------------------------------------- /sw/local/rocky8.6/noarch/rcc/modules -----------------------------------------
ansys (7)   gurobi (2)   matlab (1)   star-ccm+ (4)

---------------------------------------- /sw/local/rocky8.6/epyc3/qcif/modules -----------------------------------------
3d-dna              (1)   braker3 (1)   mtag        (1)   salsa2  (1)   shpc (1)
biobakery_workflows (1)   gtdbtk  (1)   rmats-turbo (1)   shovill (1)

---------------------------------------- /sw/local/rocky8.6/noarch/qcif/modules ----------------------------------------
blast    (1)   hisat2    (1)   mixer       (1)   ont-fast5-api (1)   sra-tools    (1)   trinotate (1)
f5c      (1)   kallisto  (1)   mlst        (1)   repeatmasker  (1)   star         (1)   xpore     (1)
fastool  (1)   kofamscan (1)   nanocompore (1)   repeatmodeler (1)   transdecoder (1)
gff3sort (1)   ldsc      (1)   nanopolish  (1)   rsem          (1)   trinity      (2)

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
|prokka|10|RCC|YES|
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

* DIA-NN
* Mr Bayes
* VBZ Compression Tool
* LESYMAP
* 
