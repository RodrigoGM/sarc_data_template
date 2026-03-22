# seqdata/

## Purpose
This directory holds **raw FASTQ files only**.

---
## Rules
1. **No BAM, BED, CSV, or any derived file** — those belong in `results/`.
2. **No PHI in file names.** Use deidentified sample IDs (e.g., `P001`).
3. Generate and include `checksums.txt` so recipients can verify integrity:
   ```bash
   find -name '*.fastq.gz' -exec md5sum {} \; >> checksums.txt
   ```
4. Ideally include in an example directory tree 
---

## Sequencing modalities and file detail:
- [ ] Select only those used in the study.  technical description of the data under each modality, e.g. 
- [ ] metadata/deidentified.sequence.metadata.csv should contain data and notes pertinent to sample collection, and sample quality
- [ ] metadata/deidentified.clinical.phenotype.csv contains patient responses and other measured or estimated phenotypes 

### msk_impact/
Standard impact run of one sample per patient, across 20 patients acros two time points : total 40 samples.
Files/directories are named as <patient_id>_<sample_id>_<time_point>_<other>...

```
msk_impact/
├── P01_tp1_/
│   ├── P01_tp1_IGO_XXXXX_A_S000_L001_001_R1.fastq.gz
│   ├── P01_tp1_IGO_XXXXX_A_S000_L001_001_R2.fastq.gz
│   ├── P01_tp1_IGO_XXXXX_A_S000_L002_001_R1.fastq.gz
│   └── P01_tp1_IGO_XXXXX_A_S000_L002_001_R2.fastq.gz
├── P01_tp2_/
│   ├── P01_tp2_IGO_XXXXX_B_S000_L001_001_R1.fastq.gz
│   ├── P01_tp2_IGO_XXXXX_B_S000_L001_001_R2.fastq.gz
│   ├── P01_tp2_IGO_XXXXX_B_S000_L002_001_R1.fastq.gz
│   └── P01_tp2_IGO_XXXXX_B_S000_L002_001_R2.fastq.gz
├── P02_tp1_/
│   ├── P02_tp1_IGO_XXXXX_Y_S000_L001_001_R1.fastq.gz
│   ├── P02_tp1_IGO_XXXXX_Y_S000_L001_001_R2.fastq.gz
│   ├── P02_tp1_IGO_XXXXX_Y_S000_L002_001_R1.fastq.gz
│   └── P02_tp1_IGO_XXXXX_Y_S000_L002_001_R2.fastq.gz
├── ...
└── P20_tp2_/
    ├── P20_tp1_IGO_XXXXX_Z_S000_L001_001_R1.fastq.gz
    ├── P20_tp1_IGO_XXXXX_Z_S000_L001_001_R2.fastq.gz
    ├── P20_tp1_IGO_XXXXX_Z_S000_L002_001_R1.fastq.gz
    └── P20_tp1_IGO_XXXXX_Z_S000_L002_001_R2.fastq.gz
```
### bulk_wgs/

```
wgs/
├── Project_XXXXX
│   ├── acl_permissions.txt
│   ├── BONO_0103
│   │   ├── Sample_P0000_01FC_P0_t1_IGO_XXXXX_82
│   │   │   ├── P0000_01FC_P0_t1_IGO_XXXXX_82_S107_L003_R1_001.fastq.gz
│   │   │   ├── P0000_01FC_P0_t1_IGO_XXXXX_82_S107_L003_R2_001.fastq.gz
│   │   │   ├── P0000_01FC_P0_t1_IGO_XXXXX_82_S107_L004_R1_001.fastq.gz
│   │   │   ├── P0000_01FC_P0_t1_IGO_XXXXX_82_S107_L004_R2_001.fastq.gz
│   │   │   └── ...
│   │   ├── Sample_P0000_01QE_P0_t1_IGO_XXXXX_16
│      │   │   ├── P0000_01QE_P0_t1_IGO_XXXXX_16_S105_L003_R1_001.fastq.gz
│      │   │   ├── P0000_01QE_P0_t1_IGO_XXXXX_16_S105_L003_R2_001.fastq.gz
│      │   │   └── ...
│      │   ├── Sample_P0000_01QK_P0_t1_IGO_XXXXX_14
│      │   │   ├── P0000_01QK_P0_t1_IGO_XXXXX_14_S104_L003_R1_001.fastq.gz
│      │   │   ├── P0000_01QK_P0_t1_IGO_XXXXX_14_S104_L003_R2_001.fastq.gz
│      │   │   └── ...
│      │   └── Sample_P0000_01QN_P0_t2_IGO_XXXXX_21
├── Project_XXXXX_X
│   ├── acl_permissions.txt
│   ├── BONO_0036
│   └── BONO_0037
├── Project_XXXXX_Y
│   ├── acl_permissions.txt
│   ├── FAUCI2_0087
│   └── FAUCI2_0089
├── Project_XXXXX_Z
│   ├── acl_permissions.txt
│   ├── FAUCI2_0087
│   └── FAUCI2_0089
├── sync_XXXXX.log
└── sync_igo_XXXXX.sh
```
### bulk_wes/
### bulk_rna/

### single_cell_rnaseq/
10X single-cell run of tumor biopsies and PBMC sample per patient, across 29 patients across two time points with replicates: total 167 samples.  
PBMC were collected starting at P35; some have TCR (as VDJ|TCR) and/or BCR sequencing.

Files/directories are named as <patient_id>_<trt_cycle>_<day_of_trt>_<{"",PBMC}>_<replicate>_...

```
tree single_cell_rnaseq/
├── Sample_P14_C0_D0_01_IGO_XXXXX_1
│   ├── P14_C0_D0_01_IGO_XXXXX_1_S3_L001_R1_001.fastq.gz
│   ├── P14_C0_D0_01_IGO_XXXXX_1_S3_L001_R2_001.fastq.gz
│   ├── P14_C0_D0_01_IGO_XXXXX_1_S3_L002_R1_001.fastq.gz
│   └── P14_C0_D0_01_IGO_XXXXX_1_S3_L002_R2_001.fastq.gz
├── Sample_P14_C0_D0_02_IGO_XXXXX_2
│   ├── P14_C0_D0_02_IGO_XXXXX_2_S4_L001_R1_001.fastq.gz
│   ├── P14_C0_D0_02_IGO_XXXXX_2_S4_L001_R2_001.fastq.gz
│   ├── P14_C0_D0_02_IGO_XXXXX_2_S4_L002_R1_001.fastq.gz
│   └── P14_C0_D0_02_IGO_XXXXX_2_S4_L002_R2_001.fastq.gz
├── ...
└── Sample_P45_C3_D64_PBMC_01_VDJ_IGO_XXXXX_CA_1
    ├── P45_C3_D64_PBMC_01_VDJ_IGO_XXXXX_CA_1_S16_L001_I1_001.fastq.gz
    ├── P45_C3_D64_PBMC_01_VDJ_IGO_XXXXX_CA_1_S16_L001_I2_001.fastq.gz
    ├── P45_C3_D64_PBMC_01_VDJ_IGO_XXXXX_CA_1_S16_L008_I2_001.fastq.gz
    ├── P45_C3_D64_PBMC_01_VDJ_IGO_XXXXX_CA_1_S16_L008_R1_001.fastq.gz
    └── P45_C3_D64_PBMC_01_VDJ_IGO_XXXXX_CA_1_S16_L008_R2_001.fastq.gz

167 directories, 2503 files

```

### spatial_rnaseq/

### single_cell_cnv/
