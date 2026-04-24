# List of Datasets

**Updated: 19 June 2025**

To save on disk space, and reduce duplication of effort, a growing number of datasets are being made available.
They are being provided centrally in Bunya scratch filesystem.

For more information, please refer to these documents
- [Operational Procedures](https://github.com/UQ-RCC/hpc-docs/blob/main/policy/Bunya-User-Data-Spaces-Operational-Procedure.md#scratchopendata)
- [User Data Guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-UserData-Guide.md#scratchopendata)

Most are freely available to use. Some require agreement to license conditions.

## Licensed Data Sets

To gain access to these licensed data sets, please submit an email to rcc-support@uq.edu.au to request it.

```
/scratch/licenseddata/
└── imagenet
    ├── imagenet-10k
    ├── imagenet-1k
    └── imagenet-21k

4 directories
```

## Open Data Sets

### Protein Folding

```
/scratch/opendata/protein
├── AlphaFold
│   ├── databases
│   ├── databases_3
│   └── model_3
├── ColabFold
│   ├── database
│   └── database_gpu
├── LocalColabFold
│   └── params
├── OpenFold
│   ├── openfold3
│   ├── openfold_params
│   └── openfold_soloseq_params
├── bagel
│   ├── models--facebook--esm2_t33_650M_UR50D
│   └── models--facebook--esmfold_v1
├── boltzgen
│   ├── datasets--boltzgen--inference-data
│   ├── hub
│   ├── models--boltzgen--boltzgen-1
│   └── xet
├── chai-lab
│   ├── esm
│   └── models_v2
├── mmseqs
│   └── NR
└── proteina-complexa
    └── community_models

28 directories
```

### Genomics

```
/scratch/opendata/genomics
├── AllTheBacteria
│   └── atb.lmi
├── AntiFam -> ProteinSequenceDatabases/AntiFam
├── BLAST
│   ├── Betacoronavirus
│   ├── NIH
│   ├── UniProt
│   ├── env_nr
│   ├── human_genome
│   ├── mouse_genome
│   ├── nr
│   ├── nt
│   ├── nt_euk
│   ├── nt_prok
│   ├── nt_viruses
│   ├── patnt
│   ├── ref_euk_rep_genomes
│   ├── ref_prok_rep_genomes
│   ├── refseq_protein
│   ├── refseq_rna
│   ├── refseq_select_prot
│   ├── tsa_nr
│   └── tsa_nt
├── Bakta
│   └── v6
├── BinChicken
│   ├── checkm2
│   ├── gtdbtk
│   ├── singlem
│   └── taxonomy
├── Biobakery
│   └── 3.1
├── Centrifuge
│   ├── LLNL-nt
│   ├── nt-20180303
│   ├── p+h+v-20161200
│   └── p-compressed-20180415
├── CheckM2
│   ├── version_2
│   └── version_3
├── DRAM_data
│   ├── kofam_profiles
│   ├── tmp
│   └── vogdb_hmms
├── EggNOG
│   └── emapperdb-5.0.2
├── GTDB
│   ├── release220 -> releases/release220
│   ├── release226 -> releases/release226
│   └── releases
├── HISAT2
│   ├── bdgp6
│   ├── bdgp6_tran
│   ├── ce10
│   ├── dm6
│   ├── grch38
│   ├── grch38_rep
│   ├── grch38_snp
│   ├── grch38_snp_rep
│   ├── grch38_snp_tran
│   ├── grch38_tran
│   ├── grcm38
│   ├── grcm38_snp
│   ├── grcm38_snp_tran
│   ├── grcm38_tran
│   ├── hg38
│   ├── hg38_tran
│   ├── mm10
│   ├── r64
│   ├── r64_tran
│   ├── rn6
│   ├── sc3
│   ├── wbcel235
│   └── wbcel235_tran
├── Humann
│   └── Humann4
├── KOfam -> ProteinSequenceDatabases/KOfam
├── Kraken2
│   ├── RNA
│   ├── Refseq
│   └── Uniq
├── METABOLIC
│   └── METABOLIC_v4.0
├── Metabuli
│   └── version_1
├── Metagenomics
│   ├── chocophlan
│   ├── humann_example
│   ├── uniref
│   └── utility_mapping
├── Metaphlan
│   └── Metaphlan4
├── Pfam -> ProteinSequenceDatabases/Pfam
├── ProteinSequenceDatabases
│   ├── AntiFam
│   ├── KOfam
│   └── Pfam
├── RefSeqGenBank
│   └── genbank
├── RoseTTAFold
│   ├── Software
│   ├── UniRef30_2020_06
│   ├── bfd
│   ├── pdb100_2021Mar03
│   └── weights
├── SingleM
│   ├── 3.2.1
│   ├── 4.3.0
│   └── 5.4.0
├── UniProt
│   └── UniRef
└── kneadData
    ├── Homo_sapiens_hg37_and_human_contamination_Bowtie2_v0.1
    ├── Homo_sapiens_hg38_transcriptome_Bowtie2_v0.1
    ├── Homo_sapiens_hg39_T2T_Bowtie2_v0.1
    ├── SILVA_128_LSUParc_SSUParc_ribosomal_RNA_v0.2
    └── mouse_C57BL_6NJ_Bowtie2_v0.1

117 directories
```
### Machine Learning

```
/scratch/opendata/models
├── ComfyUI
│   └── models
├── gguf
│   ├── aya-expanse-8b
│   ├── codellama-70b
│   ├── cogito-70b
│   ├── deepcoder-14b
│   ├── granite3.1-dense-8b
│   ├── granite3-dense-8b
│   ├── granite3-moe-1b
│   ├── granite3-moe-3b
│   ├── granite-code-34b
│   ├── llama3.1-405b
│   ├── llama3.1-405b-instruct-fp16
│   ├── llama3.1-70b
│   ├── llama3.2-3b
│   ├── llama3.2-vision-90b
│   ├── llama3.3-70b-instruct-fp16
│   ├── mistral-large-123b
│   ├── phi3-medium
│   └── qwen2.5-coder-32b
├── huggingface
│   └── Qwen2.5-Coder-32B-Instruct
├── modelzoo
│   └── checkpoints
├── ollama
│   ├── blobs
│   └── manifests
└── sd3.5
    ├── text_encoder
    └── VAE

31 directories
```

```
/scratch/opendata/model-datasets/
├── broken_nuScenes-C
│   ├── beam_missing
│   ├── cross_sensor
│   ├── crosstalk
│   ├── fog
│   ├── incomplete_echo
│   ├── motion_blur
│   ├── snow
│   └── wet_ground
├── nuScenes -> Robo3D/data/sets/nuscenes
├── nuscenes-c
│   ├── Brightness
│   ├── CameraCrash
│   ├── ColorQuant
│   ├── Fog
│   ├── FrameLost
│   ├── LowLight
│   ├── MotionBlur
│   └── Snow
├── Robo3D
│   ├── create
│   ├── data
│   ├── docs
│   └── zoo
└── RoboBEV
    ├── corruptions
    ├── docs
    ├── log
    ├── pyenv
    ├── uda
    └── zoo

31 directories
```

## HOW TO UPDATE THIS INFORMATION

Information on this web page will be updated sporadically. 
If you need to know the latest, here is how you can look it up for your self.

```
tree -d -L 2 /scratch/licenseddata/

tree -d -L 2 /scratch/opendata/protein
tree -d -I Downloads -L 2 /scratch/opendata/genomics

tree -d -L 2 /scratch/opendata/models
tree -d -L 2 /scratch/opendata/model-datasets
```
