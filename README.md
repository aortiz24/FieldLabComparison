# FieldLabComparison

Scripts for microbiome analysis of bacterial 16S sequences from ants.

**Data:** 
* SRA accessions:
	* PRJNA170251 (Mycocepurus): metadata in SRA correct, `data/SraRunTableSRP018247.txt`
	* PRJNA170250 (Trachymyrmex/Cyphomyrmex): metadata in SRA is not correct, revised metadata in `data/SraRunTableSRP018246corrected.txt` 
* Silva database:
	* Use [Full length sequences and taxonomy references](https://www.mothur.org/wiki/Silva_reference_files) for version 128, which includes taxonomy file. The `silva.nr_v128.tax` file and `silva.nr_v128.align` file need to be moved to the `silva/`. Another option is to use the `silva.bacteria.fasta` which is a silva reference file from the MiSeq SOP. The `silva.bacteria.fasta` file can be trimmed to the V1-V3 region using the align.seqs() and the `E.coliV1V3.fas` file.

**Dependencies:**
* [SRA Toolkit v2.8.1or higher](https://github.com/ncbi/sra-tools) for data download
* [seq_crumbs](https://bioinf.comav.upv.es/seq_crumbs/) only if using `dataCheck.sh` 
* [MothuR](https://mothur.org/wiki/Download_mothur) for raw data cleaning and OTU assessment

**Analysis Design**
* MothuR analysis based on [454](https://www.mothur.org/wiki/454_SOP) and [MiSeq](https://www.mothur.org/wiki/MiSeq_SOP) tutorials to create OTU table
* Visualization and hypothesis testing in R

**Workflow**
* `dataDownload.sh` download data from NCBI SRA (takes several minutes depending on internet connectivity)
	* `data/dataCheck.sh` check SRA data against archived sequence files, do not need to run again
* `mothur_SilvaRef.bat` create custom Silva alignment for reference (takes ~10 minutes)
* `mothur_prep.sh` split, trim, and aggregate sequence files (takes several minutes)
* `mothur_otu.bat` processes combined sequences and outputs OTU table
