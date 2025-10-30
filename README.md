# Project 2: M. tuberculosis Comparative Genomics (PAS Resistance)

* **Author: Youssef Mimoune**
* **Date: 26-Oct-2025**

---

## 1. Project Objective

This project performs a complete bioinformatics analysis to identify the genetic cause of Para-aminosalicylic acid (PAS) resistance in a clinical *Mycobacterium tuberculosis* sample (`DRR749572`).

The analysis compares the resistant genome to a known drug-sensitive (control) genome (`DRR749571`).

## 2. Bioinformatics Pipeline

The entire analysis was performed using a series of Jupyter Notebooks:

1.  **[01_Download_Data.ipynb](notebooks/01_Download_Data.ipynb):** Fetched raw FASTQ data from the SRA database.
2.  **[02_QC_and_Trimming.ipynb](notebooks/02_QC_and_Trimming.ipynb):** Used `fastp` to assess read quality and trim adapters.
3.  **[03_Genome_Assembly.ipynb](notebooks/03_Genome_Assembly.ipynb):** Assembled the trimmed reads into complete genomes using `SPAdes`.
4.  **[04_Genome_Annotation.ipynb](notebooks/04_Genome_Annotation.ipynb):** Annotated the assembled genomes using `Prokka` to find all genes.
5.  **[05_Comparative_Analysis.ipynb](notebooks/05_Comparative_Analysis.ipynb):** Performed a **hypothesis-driven** search for known resistance mutations.
6.  **[06_Pangenome_Roary.ipynb](notebooks/06_Pangenome_Roary.ipynb):** Performed an **unbiased** search to find all differences in the core genome.

---

## 3. Results & Scientific Conclusion

### Finding 1: Hypothesis-Driven Search (FAIL)

The primary mechanism of PAS resistance involves mutations in the folate pathway. An investigation (Notebook 05) was conducted on the protein sequences of the five main canonical target genes:
* `folP1` (Dihydropteroate synthase)
* `folP2` (Inactive dihydropteroate synthase 2)
* `folC` (Dihydrofolate synthase)
* `thyA` (Thymidylate synthase)
* `ribD` (Riboflavin biosynthesis protein)

**Result:** All five genes were **100% identical** at the protein level between the resistant and control strains. This definitively proves that the resistance is **non-canonical**.

### Finding 2: Unbiased Pangenome Search (SUCCESS)

A pangenome analysis (Notebook 06) was performed using `Roary` to align all core genes (3,967 genes) shared by both strains.

The `snp-sites` tool was then used to scan this 3.8 Mbp alignment for all differences.

**Result:** The analysis identified **exactly 11 Single Nucleotide Polymorphisms (SNPs)** in the entire core genome.

### Final Conclusion

The PAS resistance in sample `DRR749572` is caused by a **novel or non-canonical mechanism**. The causative mutation is **one of these 11 identified SNPs**, which are located in genes not previously associated with PAS resistance.

---

## 4. How to Run

This project is fully reproducible.

1.  Clone the repository:
    ```bash
    git clone https://github.com/refmyoussef-source/Mtb_Genomic_Analysis-.git
    ```
2.  Create and activate the Conda environment:
    ```bash
    mamba env create -f environment.yml
    mamba activate assembly_env
    ```
3.  Launch Jupyter Lab and run the notebooks in order:
    ```bash
    jupyter lab
    ```
