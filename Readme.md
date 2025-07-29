Variant Annotation and ACMG Classification Pipeline

This repository contains a pipeline for processing variant annotation files, performing ACMG-based classification, and extracting specific gene data for downstream analysis. The scripts are implemented in R and are designed to efficiently handle multiple input files.



Table of Contents

1. Overview

2\. File Structure

3\. Prerequisites

4\. Scripts and Workflow

5\. How to Run the Scripts

6\. Output Files

7\. Contributing

8\. License

9\. Overview

The pipeline processes variant annotation files (e.g., .txt or .multianno.txt) to:



Perform allele frequency consistency checks and classify variants using ACMG criteria.

Extract specific genes from the dataset based on user-defined lists.

Consolidate results into a single Excel sheet for further analysis.

The workflow is modular, allowing flexibility for customization and integration with other pipelines.



File Structure



├── README.md                     # This file

├── Scripts/

│   ├── add\_AFS\_Para.R            # Adds the AFS\_Para column based on allele frequency parameters

│   ├── reorder\_columns.R         # Reorders columns to bring key fields to the front

│   ├── assign\_A\_CMG.R            # Assigns ACMG classifications based on rules

│   ├── extract\_genes.R           # Extracts specific genes and consolidates results

├── Data/

│   ├── Input/                    # Directory for input files (variant annotation files)

│   ├── Output/                   # Directory for processed output files

├── Lit.parameters\_acmg\_83\_wes\_feb.xlsx  # Reference Excel file for gene-specific annotations



Prerequisites

Software Requirements

1. R (version 4.0 or higher): Install R from https://www.r-project.org/ .

2\. RStudio (optional but recommended): Install from https://www.rstudio.com/ .

R Packages

Install the following R packages if not already installed:





install.packages("readxl")    # For reading Excel files

install.packages("openxlsx")  # For writing Excel files



Input Files

Place all input files in the Data/Input/ directory.

Ensure the reference Excel file (Lit.parameters\_acmg\_83\_wes\_feb.xlsx) is in the root directory.



Scripts and Workflow

1\. Add AFS\_Para Column

&nbsp;	Script: add\_AFS\_Para.R

&nbsp;	Purpose: Adds the AFS\_Para column based on allele frequency parameters (ExAC\_ALL\_AF, ExAC\_SAS\_AF, esp\_AF, g1000\_AF).

&nbsp;	Logic:

&nbsp;	If 3 or more parameters are PM2, assign PM2.

&nbsp;	If 3 or more parameters are BS2, assign BS2.

&nbsp;	If 3 or more parameters are NA, assign NA.

&nbsp;	If 2 parameters are PM2 and 2 are BS2, assign PM2.

2\. Reorder Columns

&nbsp;	Script: reorder\_columns.R

&nbsp;	Purpose: Moves key columns (AFS\_Para, Lit, Pfam, Variant\_Classification, ExonicFunc.refGene, AAChange.refGene) to the front for better readability.

3\. Assign ACMG Classifications

&nbsp;	Script: assign\_A\_CMG.R

&nbsp;	Purpose: Assigns ACMG classifications (A\_CMG) based on predefined rules involving AFS\_Para, Lit, Pfam, and Variant\_Classification.

4\. Extract Specific Genes

&nbsp;	Script: extract\_genes.R

&nbsp;	Purpose: Filters rows containing specific genes (from AAChange.refGene) and consolidates the results into a single Excel file.

&nbsp;	Key Columns in Output:

&nbsp;		Sample: Sample name extracted from the file name.

&nbsp;		A\_CMG: ACMG classification.

&nbsp;		AAChange.refGene: Amino acid change information.

&nbsp;		ExonicFunc.refGene: Functional annotation of the variant.

&nbsp;		Gene: Extracted gene name.

How to Run the Scripts

Step 1: Prepare Input Files

&nbsp;	Place all input files in the Data/Input/ directory.

&nbsp;	Ensure the reference Excel file (Lit.parameters\_acmg\_83\_wes\_feb.xlsx) is in the root directory.

Step 2: Run the Scripts

&nbsp;	Open R or RStudio.

&nbsp;	Set the working directory to the root folder of this repository:

&nbsp;	setwd("path/to/your/repo")

&nbsp;	Run the scripts in the following order:



&nbsp;	source("Scripts/add\_AFS\_Para.R")

&nbsp;	source("Scripts/reorder\_columns.R")

&nbsp;	source("Scripts/assign\_A\_CMG.R")

&nbsp;	source("Scripts/extract\_genes.R")

Step 3: Check Output

&nbsp;	Processed files will be saved in the Data/Output/ directory.

&nbsp;	The consolidated gene extraction results will be saved as Extracted\_Genes.xlsx.

Output Files

Processed Files:

&nbsp;	Each input file is processed and saved in the Data/Output/ directory with updated columns (AFS\_Para, A\_CMG, etc.).

Consolidated Gene Extraction:

&nbsp;	A single Excel file (Extracted\_Genes.xlsx) containing:

&nbsp;		Sample: Sample name.

&nbsp;		A\_CMG: ACMG classification.

&nbsp;		AAChange.refGene: Amino acid change information.

&nbsp;		ExonicFunc.refGene: Functional annotation of the variant.

&nbsp;		Gene: Extracted gene name.

Contributing

Contributions are welcome! If you have suggestions for improvements or encounter any issues, please open an issue or submit a pull request.



License

This project is licensed under the MIT License. See the LICENSE file for details.

