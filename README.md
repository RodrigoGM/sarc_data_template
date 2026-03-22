# <PROJECT TITLE> — Data Sharing Repository

> **⚠️ WARNING: This repository must NEVER contain Protected Health Information (PHI).
> See [CHECKLIST.md](CHECKLIST.md) before adding or modifying any file.**

---

## Project Overview
Example fields:

| Field                  | Value                                                       |
|------------------------|-------------------------------------------------------------|
| **IRB Protocol**       | `XX-XXX`                                                    |
| **IGO Project ID**     | _e.g., XXXXX_                                               |
| **PI**                 | _Principal Investigator Name(s)_                            |
| **Project Name**       | _e.g., TIL therapy in sarcomas_                             |
| **Sequencing Methods** | 10X scRNA-seq, 5′ Gene Expression, bulk RNA-seq, MSK-IMPACT |
| **Target Cells**       | 20,000 per capture well                                     |
| **Additional VDJ**     | BCR + TCR _(if applicable)_                                 |
| **Chemistry**          | _e.g., 10X Chromium v3.1 or newer_                          |
| **Experimental Info**  | ...                                                         |


---

## To use this data contact
| Role                      | Names & Emails |
|---------------------------|----------------|
| **Lead Contacts:**        |                |
| **Data Access:**          |                |
| **Bioinformatics:**       |                |
| **Statistics:**           |                |
| **Clinical Coordinator:** |                |

> **Do NOT list personal email addresses or real names in public repositories unless you have prior approval by the individuals you'll list**


---

## Study Design (Example)

_Brief plain-language description of the clinical trial, its arms, and the
sequencing rationale. Clinicians should be able to read this section and
understand what data lives here.  Include the reference of published works 
that make use of this repository as well._
 

- **Indication**: _e.g., Soft tissue sarcoma_
- **Treatment arms**: _e.g., Drug A + Drug B_
- **Biopsy schedule**: _e.g., Screening (Day −7) and On-treatment (Day 15)_
- **Blood draws**: _e.g., 6 time points per participant_
- **Matched samples**: Biopsy + PBMC submitted per patient per time point

---

## Repository Layout

_Brief plain-language description of the the repo structure and analysis carried 
 out. This first parragraph is intended for a broad audience, including clinitcians,
 other principal investigators, and admins.
 
 Then, include a technical summary of the current work. This section is intended 
 for a computational biology and bioinformatic audince is likely to use the data.
 Thus, this section is directly intended to create a succesful data transfer for
 derived works even in the absence of the project leads._ 


```
<project_title>
├── README.md
├── CHECKLIST.md
├── seqdata/
│   ├── README.md
│   ├── bulkRNA/
│   ├── single-cell/
│   ├── msk-impact/
│   └── (FASTQ files only; optionally nested by project/run)
├── results/
│   ├── README.md
│   ├── 01_qc/
│   │   └── README.md
│   ├── 02_alignment/
│   │   └── README.md
│   ├── 03_count_matrices/
│   │   └── README.md
│   ├── 04_downstream_analysis_1/
│   │   └── README.md
│   ├── 05_downstream_analysis_2/
│   │   └── README.md
│   ├── .../
│   │   └── README.md
│   └── 99_reports_for_noncomputing/
│       └── README.md
└── metadata/
    ├── README.md
    ├── samplesheet.csv
    ├── deidentified.clinical.phenotypes.csv
    └── deidentified.sequence.metadata.csv
```

## Additional Data Transfer Details

...