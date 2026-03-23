# Data Sharing Checklist

**Document:** CHECKLIST.> **Version: 1.0.0** | Last updated: YYYY-MM-DD

This document defines the rules, instructions, and submission checklist for
every contributor. 
**Read this entirely before adding or modifying files to your project repo.**

---

## Table of Contents

1. [Global rules](#1-global-rules)
2. [Requiered Files](#2-required-files)
3. [Directory requirements](#3-directory-requirements)
   - [seqdata/](#31-seqdata)
   - [metadata/](#32-metadata)
   - [results/](#33-results)
4. [Pre-release validation](#4-pre-release-validation)
5. [Version History](#6-version-history)

---


## 1. Global rules (must pass)
- [ ] No PHI anywhere (filenames, file contents, metadata, reports, screenshots).
- [ ] No personal emails, names, phone numbers, MRNs, accession numbers tied to a patient, or free-text clinical notes copy/pasted from a medical record.
- [ ] All IDs are de-identified and consistent across metadata tables.
- [ ] Repo contains only the required top-level structure: `seqdata/`, `results/`, `metadata/`, plus documentation files i.e. README.md & this CHECKLIST.md.
- [ ] Include an `checksums.txt` in each directory containing all sequence data and/or analysis output files, e.g. FASTQ, BAM, VCF, MAF, etc.
- [ ] Do not commit FASTQ, BAM, or any large data file into the repository
- [ ] `seqdata/` contains FASTQ files only.
- [ ] `metadata/` contains only de-identified tabular metadata.
- [ ] `results/` contains only derived outputs and must be documented per subfolder.
- [ ] `metadata/samplesheet.csv` must map every sample to FASTQ paths using relative paths and de-identified IDs.

## 2. Required files
- `README.md`
- `CHECKLIST.md`
- `seqdata/` (directory)
- `seqdata/README.md`
- `results/` (directory)
- `results/README.md`
- `metadata/samplesheet.csv`
- `metadata/deidentified.clinical.phenotypes.txt`
- `metadata/deidentified.sequence.metadata.txt`


---

## 3. Directory requirements

### 3.1 `seqdata/` (FASTQ-only)
Contains **raw sequencing reads** in FASTQ format only.  Prepare this directory under the asumption that it will be deposited in dbGAP.

**Rules**
- Only `.fastq.gz`, `README.md` documentation, `checksums.txt` (`data_download.sh` if not in README.md script) are allowed.
- No processed data BAM/CRAM, no counts, no PDFs, no spreadsheets here.

**Checklist**

- [ ] **PHI check:** Filenames contain only de-identified sample IDs (e.g., `P01`), no MRN, Path Accessions, names, initials, complete dates (Year, Month, & day), or any of the 18 HIPPA protected information fields explaned [here](https://www.hhs.gov/hipaa/for-professionals/special-topics/de-identification/index.html)
- [ ] `seqdata/README.md` explains naming conventions and directory structure, especially for comprehensive projects with multiple sequencing approaches
- [ ] FASTQ are gzip-compressed (`*.fastq.gz`)
- [ ] Pair integrity verified with tools such as `fastqc` and [check_fastq_pairs](https://github.com/RodrigoGM/check_fastq_pairs/)
- [ ] Included a `checksums.txt` at the top level
- [ ] For use sequencing modality as directory names to organize the data 
	- [ ] `bulk_rna/`
	- [ ] `msk_impact/`
	- [ ] `bulk_wgs`
	- [ ] `bulk_wes`
	- [ ] `single_cell_rnaseq`
	- [ ] `single_cell_cnv`
	- [ ] etc...
- [ ] Every FASTQ listed in `metadata/samplesheet.csv` exists at the path provided


---

### 3.2 `metadata/` (de-identified tables only)
**Rules**
- No PHI, no free-text clinical narratives copy-pasted from a medical record.
- Use a comma separated values format only (`.csv`).
- Must be internally consistent: sample IDs match exactly across files, FASTQ, and results files.

Sample IDs in filenames must be opaque (no MRN, no initials)                                                   |

#### `samplesheet.csv`
This file was inspired by nf-core.  Ideally use a samplesheet that's compatible with the primary sequencing technology; or add additional sample sheets (e.g. samplesheet_scrnaseq.csv, samplesheet_wes.csv, etc) for comprehensive projects involving multiple sequencing types e.g. single-cell-rnaseq, bulk-rnaseq, msk-impact, bulk_wes, spatial_rnaseq.

| Requirement          | Details                                                             |
|----------------------|---------------------------------------------------------------------|
| **Format**           | Comma-separated, UTF-8, Unix or DOS line endings                    |
| **Required columns** | `sample`, `fastq_1`, `fastq_2`                                      |
| **Optional columns** | additional nf-core fields (https://nf-co.re)                        |
| **Paths**            | Relative to repository root (e.g., `seqdata/P001_...`)              |
| **PHI check**        | No patient identifiers in any column                                |
| **Consistency**      | Every `sample` value must match entries in the other metadata files |

#### `deidentified.clinical.phenotypes.csv`
This file should contain the clinical outcomes and other phenotypes relevant to a clinical trial. File records are per patient.  Additional companion files are permited e.g. `deidentified.spiderplot.csv`, a long-format relative date file useful for spider plots to asses the duration of response across individuals.  

| Requirement          | Details                                                             |
|----------------------|---------------------------------------------------------------------|
| **Format**           | Comma-separated, UTF-8, Unix or DOS line endings                    |
| **Required columns** | `patient.id`, `trt`, `pfs`, `best.overall.response`                 |
| **For ages e.g. `age of diagnosis`** | Write in years, e.g. 50; any age greater than 89 must be labeled as 89+ |
| **For timepoints**   | Use relative offsets only (`day 0`, `day 28`; or week 0`, `week 4`) — no calendar dates in the repo.  E.g. number of days relative to baseline, screening, 1st day of treatment  |
| **Notes**            | Free-text notes relevant to the data analysis or interpretation from a bioinformatitian or statistician |
| **PHI check**        | Must pass a manual review for all 18 HIPAA identifiers              |
| **Consistency**      | Every `sample` value must match entries in the other metadata files |

**WARNING:** Year of birth is discuraged, but not strictly prohibited, however, disclosing ages above 90 is prohibited, making year of birth an potential violation of HIPPA rules.

#### `deidentified.sequence.metadata.txt`
This file should contain the information relevant to the data collection. File records are per sample or replicate, whichever is applicable.

| Requirement          | Details                                               |
|----------------------|-------------------------------------------------------|
| **Format**           | Tab-delimited, UTF-8, Unix line endings               |
| **Required columns** | `patient.id`, `sample.id`, `timepoint`, `lab notes`, `clinical notes` |
| **For timepoints**   | Relative offsets only (e.g., `day0`, `day30`)         |
| **Lab Notes**        | Relevant information when processing the sample, can be as individual columns e.g. `viability`, or free text e.g. `Lab Notes: sample arrived fresh on ice instead of frozen, flash frozen in lab` |
| **Clinical Notes**   | Notes from the clinic relative to the interpretation to the data and non-redundant with clinical phenotypes. e.g. `patient had a seizure during biopsy collection`|
| **PHI check**        | No operator names; use role titles if needed          |

**Checklist**

- [ ] `metadata/samplesheet.csv` exists and is self-described (column meanings documented in `metadata/README.md`).
- [ ] `metadata/samplesheet.csv` uses relative paths to FASTQs in `seqdata/`.
- [ ] `metadata/deidentified.clinical.phenotypes.txt` exists and contains only de-identified fields.
- [ ] `metadata/deidentified.sequence.metadata.txt` exists and contains only de-identified fields.
- [ ] No columns contain patient identifiers (MRN, full dates, address), and no unreviewed free-text fields. [Review PHI fields](https://www.hhs.gov/hipaa/for-professionals/special-topics/de-identification/index.html) when in doubt.
- [ ] Missing values use a consistent token (recommended: `NA` or `.` or `-`).

---

### 3.3 `results/` (derived outputs only)
**Rules**
- Everything in `results/` must be reproducible from `seqdata/` via documented pipelines.
- Each subfolder must be self-explanatory and include a `README.md`.

| Requirement               | Details                                                                                                         |
|---------------------------|-----------------------------------------------------------------------------------------------------------------|
| **Sub-folder naming**     | Lowercase, underscores, descriptive with a number prefix (e.g., `03_differential_expression/`)                  |
| **README per sub-folder** | Each must contain a `README.md` stating: tool name, version, genome build, key parameters, and date of analysis |
| **Figures**               | Must not embed PHI in titles, legends, or EXIF metadata                                                         |
| **Large files**           | Do not commit lare files to the repo if publishing on github                                                    |
| **Reproducibility**       | Include the exact command or config file used to generate results in the readme                                 |
| **BAM / CRAM**.           | Sorted, indexed; index file (`.bai`/`.crai`) must accompany the alignment                                       |
| **Images (PNG/PDF/SVG)**  | Strip EXIF metadata; no PHI in embedded text layers                                                             |
| **R / Python scripts**    | No hard-coded absolute paths; no credentials or API keys                                                        |


**Checklist**

- [ ] `results/README.md` describes overall structure and how results were generated.
- [ ] Each subfolder (e.g., `01_qc/`, `02_alignment/`, etc) has a `README.md` describing:
  - [ ] Inputs
  - [ ] Software/pipeline + versions
  - [ ] Key outputs and where to find them
- [ ] Any human-facing summaries are placed in `results/99_reports_for_non_computational/`.
- [ ] No PHI anywhere; including plots, tables, embedded labels, etc.

---

## 4. Pre-release validation
- [ ] Run a manual scan of filenames for prohibited patterns (names, MRN-like strings, DOB-like dates).
- [ ] Spot-check metadata cells for forbidden identifiers.
- [ ] Confirm `samplesheet.csv` rows match FASTQ files exactly (no broken paths).
- [ ] Tag release (e.g., `v1.0.0`) only after checklist passes, and version bump after a publication when the new the results are added and shared.

## 5. Version history

### v1.0.0 | Release date: 2025-03-23
