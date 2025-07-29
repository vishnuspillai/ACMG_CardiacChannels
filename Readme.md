\# 🧬 Variant Annotation and ACMG Classification Pipeline



This repository contains a pipeline for processing variant annotation files, performing ACMG-based classification, and extracting specific gene data for downstream analysis. The scripts are implemented in \*\*R\*\* and designed to efficiently handle multiple input files with a modular structure.



\## 📑 Table of Contents

1\. Overview  

2\. File Structure  

3\. Prerequisites  

4\. Scripts and Workflow  

5\. How to Run the Scripts  

6\. Output Files  

7\. Contributing  

8\. License  



\## 🔍 Overview

The pipeline processes variant annotation files (e.g., `.txt`, `.multianno.txt`) to:

\- Perform allele frequency consistency checks and classify variants using ACMG guidelines.

\- Extract specific genes from the dataset based on user-defined gene lists.

\- Consolidate results into a single Excel sheet for downstream analysis.



The workflow is \*\*modular and customizable\*\*, enabling seamless integration with other pipelines.



\## 📁 File Structure

```

├── README.md                     # This file

├── Scripts/

│   ├── add\_AFS\_Para.R            # Adds AFS\_Para column based on population AF rules

│   ├── reorder\_columns.R         # Brings key columns to the front

│   ├── assign\_A\_CMG.R            # Classifies variants based on ACMG criteria

│   ├── extract\_genes.R           # Filters specific genes and consolidates results

├── Data/

│   ├── Input/                    # Directory for input variant files

│   ├── Output/                   # Directory for processed outputs

├── Lit.parameters\_acmg\_83\_wes\_feb.xlsx  # Reference file for gene-specific rules

```



\## ⚙️ Prerequisites



\### Software

\- \[R (≥ v4.0)](https://www.r-project.org/)

\- \[RStudio](https://www.rstudio.com/) \*(optional but recommended)\*



\### R Packages

Install the following packages:

```r

install.packages("readxl")

install.packages("openxlsx")

```



\## 🔄 Scripts and Workflow



\### 1. 🧬 Add AFS\_Para Column  

\*\*Script\*\*: `add\_AFS\_Para.R`  

Adds ACMG classification based on allele frequency (`ExAC\_ALL`, `SAS`, `ESP`, `1000g`).  

\*\*Logic:\*\*

\- ≥3 AFs = PM2 → assign PM2  

\- ≥3 AFs = BS2 → assign BS2  

\- ≥3 AFs = NA → assign NA  

\- Mixed → resolve as PM2 by default  



\### 2. 📑 Reorder Columns  

\*\*Script\*\*: `reorder\_columns.R`  

Moves important columns (`AFS\_Para`, `Lit`, `Pfam`, `Variant\_Classification`, etc.) to the front.



\### 3. ⚖️ Assign ACMG Classifications  

\*\*Script\*\*: `assign\_A\_CMG.R`  

Applies ACMG rules using multiple columns (AFS\_Para, Pfam, Lit, Variant\_Classification) to assign final labels:  

\- `Pathogenic`  

\- `Likely Pathogenic`  

\- `VUS`  

\- `Likely Benign`  

\- `NA`



\### 4. 🔍 Extract Specific Genes  

\*\*Script\*\*: `extract\_genes.R`  

Filters specific genes based on `AAChange.refGene`, extracts information, and consolidates it into a master Excel file.



\*\*Key Columns:\*\*

\- `Sample`

\- `A\_CMG`

\- `AAChange.refGene`

\- `ExonicFunc.refGene`

\- `Gene`



\## 🚀 How to Run the Scripts



\### Step 1: Prepare Input  

\- Place your annotated `.txt` or `.multianno.txt` files in: `Data/Input/`  

\- Ensure `Lit.parameters\_acmg\_83\_wes\_feb.xlsx` is in the project root  



\### Step 2: Run Scripts in Order

```r

setwd("path/to/your/project")

source("Scripts/add\_AFS\_Para.R")

source("Scripts/reorder\_columns.R")

source("Scripts/assign\_A\_CMG.R")

source("Scripts/extract\_genes.R")

```



\### Step 3: Review Output  

\- Processed files → `Data/Output/`  

\- Consolidated results → `Extracted\_Genes.xlsx`



\## 📤 Output Files



\### ✅ Processed Variant Files

Each input file is saved with:

\- Updated `AFS\_Para` column

\- Final ACMG classification (`A\_CMG`)



\### ✅ Gene Extraction

Single Excel file:

\- `Extracted\_Genes.xlsx`  

\- Includes gene-specific filtered variants with annotations



\## 🤝 Contributing

Pull requests and suggestions are welcome!  

If you find bugs or have improvement ideas, feel free to \[open an issue](https://github.com/your-repo/issues).



\## 📜 License

This project is licensed under the \*\*MIT License\*\*.  

See the `LICENSE` file for full terms.



---



\*Built with ❤️ for variant interpretation workflows.\*



