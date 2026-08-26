# List of Datasets

**Updated: 26 August 2026**

To save on disk space, and reduce duplication of effort, a growing number of datasets are being made available.
They are being provided centrally in the Bunya scratch filesystem.

For more information, please refer to these documents
- [Operational Procedures](https://github.com/UQ-RCC/hpc-docs/blob/main/policy/Bunya-User-Data-Spaces-Operational-Procedure.md#scratchopendata)
- [User Data Guide](https://github.com/UQ-RCC/hpc-docs/blob/main/guides/Bunya-UserData-Guide.md#scratchopendata)

Most are freely available to use. Some require agreement to license conditions.

## Licensed Data Sets

To gain access to these licensed data sets, please submit an email to rcc-support@uq.edu.au to request it.

```
/scratch/licenseddata/
├── ADNI
│   ├── derivatives
│   └── metadata
├── alphafold3
├── imagenet
│   ├── imagenet-10k
│   ├── imagenet-1k
│   └── imagenet-21k
├── tvsd
│   └── TVSD
└── waymo
    └── waymo

12 directories
```

## Open Data Sets

### Protein Folding

```
/scratch/opendata/protein
├── alphafast
│   ├── mmcif_files
│   ├── mmseqs
│   └── mmseqs_rna
├── AlphaFold
│   ├── databases
│   ├── databases_3
│   └── model_3
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
├── ColabFold
│   ├── database
│   └── database_gpu
├── LocalColabFold
│   └── params
├── mmseqs
│   └── NR
├── OpenFold
│   ├── openfold3
│   ├── openfold_params
│   └── openfold_soloseq_params
└── proteina-complexa
    └── community_models

32 directories
```

### Genomics

```
/scratch/opendata/genomics
├── AllTheBacteria
│   └── atb.lmi
├── AntiFam -> ProteinSequenceDatabases/AntiFam
├── Bakta
│   └── v6
├── BinChicken
│   ├── checkm2
│   ├── gtdbtk
│   ├── singlem
│   └── taxonomy
├── Biobakery
│   └── 3.1
├── BLAST
│   ├── Betacoronavirus
│   ├── env_nr
│   ├── human_genome
│   ├── mouse_genome
│   ├── NIH
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
│   ├── tsa_nt
│   └── UniProt
├── Centrifuge
│   ├── LLNL-nt
│   ├── nt-20180303
│   ├── p-compressed-20180415
│   └── p+h+v-20161200
├── CheckM2
│   ├── version_2
│   └── version_3
├── diamond
├── DRAM_data
│   ├── kofam_profiles
│   ├── tmp
│   └── vogdb_hmms
├── EggNOG
│   ├── 2.1.8
│   └── emapperdb-5.0.2
├── Evo2
│   ├── hub
│   └── xet
├── GATK_legacy
│   └── GATK_indel_SNP_hg38
├── GlobDB
│   └── R232
├── GTDB
│   ├── release220 -> releases/release220
│   ├── release226 -> releases/release226
│   ├── release232 -> releases/release232
│   └── releases
├── HG
│   └── hg38
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
├── kneadData
│   ├── Homo_sapiens_hg37_and_human_contamination_Bowtie2_v0.1
│   ├── Homo_sapiens_hg38_transcriptome_Bowtie2_v0.1
│   ├── Homo_sapiens_hg39_T2T_Bowtie2_v0.1
│   ├── mouse_C57BL_6NJ_Bowtie2_v0.1
│   └── SILVA_128_LSUParc_SSUParc_ribosomal_RNA_v0.2
├── KOfam -> ProteinSequenceDatabases/KOfam
├── Kraken2
│   ├── Refseq
│   ├── RNA
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
│   ├── bfd
│   ├── pdb100_2021Mar03
│   ├── Software
│   ├── UniRef30_2020_06
│   └── weights
├── SingleM
│   ├── 3.2.1
│   ├── 4.3.0
│   ├── 5.4.0
│   └── 6.5.0
└── UniProt
    ├── releases
    └── UniRef

131 directories
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
│   ├── DeepSeek-V4-Flash
│   ├── gemma3-27b-it-abliterated
│   ├── gemma4-26b-a4b-it
│   ├── gemma4-31b-it
│   ├── GLM-4.7-iq4_xs
│   ├── gpt-oss-120b
│   ├── granite3.1-dense-8b
│   ├── granite3-dense-8b
│   ├── granite3-moe-1b
│   ├── granite3-moe-3b
│   ├── granite-code-34b
│   ├── Kimi-K2.5-BF16
│   ├── Kimi-K2.5-Q2_K_XL
│   ├── ling-1t
│   ├── ling-1t-q4_k_xl
│   ├── llama3.1-405b
│   ├── llama3.1-405b-instruct-fp16
│   ├── llama3.1-70b
│   ├── llama3.2-3b
│   ├── llama3.2-vision-90b
│   ├── llama3.3-70b-instruct
│   ├── llama3.3-70b-instruct-fp16
│   ├── minimax-m2.5-Q4_K_XL
│   ├── mistral-large-123b
│   ├── phi3-medium
│   ├── qwen2.5-72b-instruct
│   ├── qwen2.5-7b-instruct
│   ├── qwen2.5-coder-32b
│   ├── qwen3-32b
│   ├── qwen3.6-27b
│   ├── Solar-Open-100B-q4_0
│   └── Solar-Open-100B-q8_0
├── huggingface
│   ├── DeepSeek-R1-Distill-Llama-70B
│   ├── DeepSeek-V4-Flash
│   ├── Equall-Saul-7B-Instruct-v1
│   ├── Equall-SaulLM-54B-Instruct
│   ├── gemma-3-12B-it
│   ├── gemma-3-27B-it
│   ├── gemma-4-31B
│   ├── gemma-4-31B-it
│   ├── incoming
│   ├── Kimi-K2-Instruct-0905
│   ├── kosbu-Llama-3.3-70B-Instruct-AWQ
│   ├── Ling-1T
│   ├── Llama-3.3-70B-Instruct
│   ├── mesolitica-Qwen2.5-72B-Instruct-FP8
│   ├── Mistral-Small-3.2-24B-Instruct-2506
│   ├── models--amd--GLM-5.2-MXFP4
│   ├── models--moonshotai--Kimi-K3
│   ├── models--RadixArk--Kimi-K3-DSpark
│   ├── nvidia-Llama-3.3-70B-Instruct-FP8
│   ├── prithivMLmods-gemma-4-31B-it-FP8
│   ├── QuantTrio-gemma-4-31B-it-AWQ
│   ├── Qwen2.5-14B-Instruct
│   ├── Qwen2.5-72B-Instruct
│   ├── Qwen2.5-72B-Instruct-AWQ
│   ├── Qwen2.5-7B-Instruct
│   ├── Qwen2.5-7B-Instruct-AWQ
│   ├── Qwen2.5-Coder-32B-Instruct
│   ├── Qwen3-30B-A3B-Instruct-2507
│   ├── Qwen3-32B
│   ├── Qwen3-32B-AWQ
│   ├── Qwen3-32B-FP8
│   ├── Qwen3.8-27B
│   └── Qwen3-8B
├── llama.cpp
├── modelzoo
│   └── checkpoints
├── ollama
│   ├── blobs
│   ├── manifests
│   └── workshop
├── openclip
│   ├── models--apple--DFN2B-CLIP-ViT-B-16
│   ├── models--apple--DFN2B-CLIP-ViT-L-14
│   ├── models--apple--DFN5B-CLIP-ViT-H-14-378
│   ├── models--apple--MobileCLIP-B-LT-OpenCLIP
│   ├── models--laion--CLIP-convnext_base_w_320-laion_aesthetic-s13B-b82K
│   ├── models--laion--CLIP-convnext_base_w-laion2B-s13B-b82K
│   ├── models--laion--CLIP-convnext_large_d_320.laion2B-s29B-b131K-ft
│   ├── models--laion--CLIP-convnext_large_d.laion2B-s26B-b102K-augreg
│   ├── models--laion--CLIP-convnext_xxlarge-laion2B-s34B-b82K-augreg-soup
│   ├── models--laion--CLIP-ViT-B-16-CommonPool.L.laion-s1B-b8K
│   ├── models--laion--CLIP-ViT-B-16-DataComp.L-s1B-b8K
│   ├── models--laion--CLIP-ViT-B-16-DataComp.XL-s13B-b90K
│   ├── models--laion--CLIP-ViT-B-16-laion2B-s34B-b88K
│   ├── models--laion--CLIP-ViT-B-32-256x256-DataComp-s34B-b86K
│   ├── models--laion--CLIP-ViT-B-32-CommonPool.M.clip-s128M-b4K
│   ├── models--laion--CLIP-ViT-B-32-DataComp.XL-s13B-b90K
│   ├── models--laion--CLIP-ViT-B-32-roberta-base-laion2B-s12B-b32k
│   ├── models--laion--CLIP-ViT-B-32-xlm-roberta-base-laion5B-s13B-b90k
│   ├── models--laion--CLIP-ViT-bigG-14-laion2B-39B-b160k
│   ├── models--laion--CLIP-ViT-g-14-laion2B-s12B-b42K
│   ├── models--laion--CLIP-ViT-H-14-laion2B-s32B-b79K
│   ├── models--laion--CLIP-ViT-L-14-CommonPool.XL.clip-s13B-b90K
│   ├── models--laion--CLIP-ViT-L-14-DataComp.XL-s13B-b90K
│   ├── models--laion--CoCa-ViT-B-32-laion2B-s13B-b90k
│   ├── models--laion--CoCa-ViT-L-14-laion2B-s13B-b90k
│   ├── models--timm--eva02_base_patch16_clip_224.merged2b_s8b_b131k
│   ├── models--timm--eva02_enormous_patch14_clip_224.laion2b_s4b_b115k
│   ├── models--timm--eva02_large_patch14_clip_336.merged2b_s6b_b61k
│   ├── models--timm--eva_giant_patch14_clip_224.laion400m_s11b_b41k
│   ├── models--timm--resnet101_clip.openai
│   ├── models--timm--resnet101_clip.yfcc15m
│   ├── models--timm--resnet50_clip.cc12m
│   ├── models--timm--resnet50_clip.openai
│   ├── models--timm--resnet50x4_clip.openai
│   ├── models--timm--resnet50x64_clip.openai
│   ├── models--timm--ViT-B-16-SigLIP2
│   ├── models--timm--vit_base_patch16_clip_224.metaclip_2pt5b
│   ├── models--timm--vit_base_patch16_plus_clip_240.laion400m_e31
│   ├── models--timm--vit_base_patch32_clip_224.laion2b_e16
│   ├── models--timm--vit_base_patch32_clip_224.laion400m_e31
│   ├── models--timm--vit_base_patch32_clip_224.metaclip_2pt5b
│   ├── models--timm--vit_base_patch32_clip_224.openai
│   ├── models--timm--vit_huge_patch14_clip_224.metaclip_2pt5b
│   ├── models--timm--vit_large_patch14_clip_224.laion400m_e31
│   ├── models--timm--vit_large_patch14_clip_224.metaclip_2pt5b
│   ├── models--timm--vit_large_patch14_clip_224.openai
│   ├── models--timm--vit_large_patch14_clip_336.openai
│   ├── models--visheratin--nllb-clip-base-oc
│   ├── models--visheratin--nllb-clip-base-siglip
│   └── xet
├── PRISM
│   ├── colon
│   ├── kidney
│   ├── liver
│   └── pancreas
├── sd3.5
│   ├── text_encoder
│   └── VAE
└── ultralytics

140 directories
```

```
/scratch/opendata/model-datasets
├── Argoverse2
│   ├── LiDAR
│   └── Sensor
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
├── Pan-Multiplex
│   └── data
├── PRISM
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

37 directories
```

## HOW TO UPDATE THIS INFORMATION

Information on this web page will be updated sporadically. 
If you need to know the latest, here is how you can look it up for your self.

```
tree -d -I Downloads -L 2 /scratch/licenseddata/

tree -d -L 2 /scratch/opendata/protein
tree -d -I Downloads -L 2 /scratch/opendata/genomics

tree -d -L 2 /scratch/opendata/models
tree -d -L 2 /scratch/opendata/model-datasets
```
