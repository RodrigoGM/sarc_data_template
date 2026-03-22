# Data Sharing Checklist Policy (Versioned)

**Document:** CHECKLIST.md  
**Policy version:** 1.0.0  
**Effective date:** <YYYY-MM-DD>  
**Applies to:** De-identified Medical Oncology Sarcoma Service data-sharing repositories using this template

## MSKCC Policy Requirements
1. No PHI anywhere (including filenames and figures).
2. `seqdata/` contains FASTQ files only.
3. `metadata/` contains only de-identified tabular metadata.
4. `results/` contains only derived outputs and must be documented per subfolder.
5. `metadata/samplesheet.csv` must map every sample to FASTQ paths using relative paths and de-identified IDs.

## Required files
- `README.md`
- `CHECKLIST.md`
- `seqdata/` (directory)
- `results/` (directory)
- `metadata/samplesheet.csv`
- `metadata/deidentified.clinical.phenotypes.txt`
- `metadata/deidentified.sequence.metadata.txt`


# Data Sharing Checklist (Public/De-identified Repository)

This checklist is mandatory before sharing or tagging a release.

## Global rules (must pass)
- [ ] No PHI anywhere (filenames, file contents, metadata, reports, screenshots).
- [ ] No personal emails, names, phone numbers, MRNs, accession numbers tied to a patient, or free-text clinical notes.
- [ ] All IDs are de-identified and consistent across metadata tables.
- [ ] Repo contains only the required top-level structure: `seqdata/`, `results/`, `metadata/`, plus documentation files.
- [ ] Include an `checksums.txt` in each directory containing all sequence data and/or analysis output files, e.g. FASTQ, BAM, VCF, MAF, etc.
- [ ] Do not commit FASTQ, BAM, or any large data file into the repository (Except those in metadata/ or md5sum checksums.txt)

---

## Directory requirements

### `seqdata/` (FASTQ-only)
Contains **raw sequencing reads** in FASTQ format only.

**Rules**
- Only `.fastq.gz`, `README.md` documentation, `checksums.txt` (`data_download.sh` if not in README.md script) are allowed.
- No processed data BAM/CRAM, no counts, no PDFs, no spreadsheets here.

**Checklist**
- [ ] FASTQ are gzip-compressed (`*.fastq.gz`).
- [ ] Include a `checksums.txt` at the top level
- [ ] For use sequencing modality as directory names to organize the data 
	- [ ] `bulk_rna/`
	- [ ] `msk_impact/`
	- [ ] `bulk_wgs`
	- [ ] `bulk_wes`
	- [ ] `single_cell_rnaseq`
	- [ ] `single_cell_cnv`
	- [ ] etc...
- [ ] Filenames contain only de-identified sample IDs (e.g., `P01`), no names/initials/dates of birth.
- [ ] Every FASTQ listed in `metadata/samplesheet.csv` exists at the path provided.
- [ ] `seqdata/README.md` explains naming conventions and any lane/run structure.

---

### `metadata/` (de-identified tables only)
**Rules**
- No PHI, no free-text clinical narratives.
- Use tabular formats only (`.csv` or `.txt` TSV).
- Must be internally consistent: sample IDs match exactly across files.

**Checklist**
- [ ] `metadata/samplesheet.csv` exists and is self-described (column meanings documented in `metadata/README.md`).
- [ ] `metadata/samplesheet.csv` uses relative paths to FASTQs in `seqdata/`.
- [ ] `metadata/deidentified.clinical.phenotypes.txt` exists and contains only de-identified fields.
- [ ] `metadata/deidentified.sequence.metadata.txt` exists and contains only de-identified fields.
- [ ] No columns contain patient identifiers (MRN, full DOB, address), and no unreviewed free-text fields. [Review PHI fields](https://www.hhs.gov/hipaa/for-professionals/special-topics/de-identification/index.html) when in doubt.
- [ ] Missing values use a consistent token (recommended: `NA` or `.` or `-`).

---

### `results/` (derived outputs only)
**Rules**
- Everything in `results/` must be reproducible from `seqdata/` + documented pipelines.
- Each subfolder must be self-explanatory and include a `README.md`.

**Checklist**
- [ ] `results/README.md` describes overall structure and how results were generated.
- [ ] Each subfolder (e.g., `01_qc/`, `02_alignment_or_quant/`) has a `README.md` describing:
  - [ ] Inputs
  - [ ] Software/pipeline + versions
  - [ ] Key outputs and where to find them
- [ ] Any human-facing summaries are placed in `results/99_reports_for_noncomputing/`.
- [ ] No PHI anywhere; including plots, tables, embedded labels, etc.

---

## Pre-release validation
- [ ] Run a manual scan of filenames for prohibited patterns (names, MRN-like strings, DOB-like dates).
- [ ] Spot-check metadata cells for forbidden identifiers.
- [ ] Confirm `samplesheet.csv` rows match FASTQ files exactly (no broken paths).
- [ ] Tag release (e.g., `v1.0.0`) only after checklist passes.