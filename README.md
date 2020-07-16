# Metagenomics Tutorial
**Metagenomics** is the study of pooled DNA or RNA recovered from environmental sample containing organisms that have not been isolated and identified.

A **metagenome** is a collection of genomes from all the cells present in a particular environment.
*(Brock, 15th edition)*

#### First, some basics:


To analyze metagenomes several steps are required:
1. Quality check and trimming
2. Assembly
3. Binning
6. Annotation

To further improve the quality and completeness of your metagenomic reads you can perform Bin targeted reassemblies. This means you use your retrieved bins and map these back to the assembly. This might fill gaps and lengthen sequences, 



## Quality check and trimming
Removal of redundant, low quality sequences
### FastQC
### Illumina-utils

## Optional: Coverage, Diversity and similarity of metagenomic samples

- [Nonpareil](http://enve-omics.ce.gatech.edu/nonpareil/): a redundancy-based approach to assess the level of coverage in metagenomic datasets
- [Mash](): R (vegan), Pairwise distances, ordination plots 



## Optional: Abundance estimation
### Kraken2/Bracken

## Optional: Reference guided assembly

## Assembly
An assembly of short read fragments will obtain longer genomic contigs.
### Megahit

## Readmapping
### Bowtie2

## Binning
### Anvi'o

## Bin targeted reassemblies
### Spades



## Quality check and filtering

## First abundance estimation of Metagenomic reads
### using Kraken2 and Bracken

Building a Kraken database (SILVA138, GTDB, NCBI etc.)

``Kraken2-build --db NAME -special silva``

Bracken build to build a Bracken database with read length of the reads

``bracken-build -d ../../DB/Kraken2/SILVA138_db_k2/ -t 4 -l 150``

Kraken classification

``kraken2 --db ../../DB/Kraken2/SILVA138_db_k2/ --threads 4 --output Hel0_out --report report_Hel0 --paired --classified-out cseqs#.fq ../../Metagenomes/Hel_0/final_pure_reads_1.fastq ../../Metagenomes/Hel_0/final_pure_reads_2.fastq``
