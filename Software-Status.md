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

[**UNAVAILABLE DUE TO LICENSE ACCESS ISSUE**]

* Version 9.5 has been installed.
* There is an ongoing issue with accessing the Gurobi product license servers on campus.
* RCC is working with the vendor to faciliate access and use of the campus license server.
* Version 10.x will be installed once the license issue is resolved. 

Watch this space!
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
## Software Survey Requests

In late 2022, we asked users to participate in the software survey to ascertain which tools were required on Bunya.
The following table summarises the status of those requests.

_BIG TABLE_

___
## Post Software Survey Requests

These are requests that were not included in the software survey and have been requested since that time. They are necessarily lower priority.

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
ansys (7)   gurobi (1)   matlab (1)   star-ccm+ (4)

---------------------------------------- /sw/local/rocky8.6/epyc3/qcif/modules -----------------------------------------
3d-dna (1)   biobakery_workflows (1)   gtdbtk (1)   mtag (1)   rmats-turbo (1)   salsa2 (1)   shovill (1)   shpc (1)

---------------------------------------- /sw/local/rocky8.6/noarch/qcif/modules ----------------------------------------
blast   (1)   gff3sort (1)   kofamscan (1)   nanocompore   (1)   rsem      (1)   transdecoder (1)   xpore (1)
f5c     (1)   hisat2   (1)   mixer     (1)   nanopolish    (1)   sra-tools (1)   trinity      (2)
fastool (1)   kallisto (1)   mlst      (1)   ont-fast5-api (1)   star      (1)   trinotate    (1)

```
