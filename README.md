# Metagenomics Tutorial
**Metagenomics** is the study of pooled DNA or RNA recovered from environmental sample containing organisms that have not been isolated and identified.

A **metagenome** is a collection of genomes from all the cells present in a particular environment.
*(Brock, 15th edition)*

If you would like to dive deeper into the world of 'omics there are some good [Seminars](https://www.youtube.com/watch?v=R9KLkCZ95cU) from the Meren Lab. Every wednesday 4pm a new video is going live on their [Youtube Channel](https://www.youtube.com/channel/UCVFH6ULygyqqLGfDnmf0G4A).



**Before now going deeper into the analysis we will first start with some basics:**

In several steps of the tutorial you will read about "reads", "contigs", "scaffolds", etc., so here is a quick overview for you:

A **library** is a collection of similarly sized DNA fragments with known adapter sequences (20-40 bp) added to the 5' and 3' ends. The library contains your reads. 

The expression **reads** is used for single DNA or protein fragments.

**contigs** are then contiguous reads, which belong to the same genetic source and consist of two or more reads.

A **scaffold** is further a part of a reconstructed sequence containing contigs and gaps.

<p align="center">
  <img height="200" src="https://github.com/mmaeke/Metagenomics_Tutorial/blob/master/Images/Overview_MG.png" />
</p>



## Let's start with Metagenomics!

A metagenomic analysis consists of various steps: 

1. Your sample hast to be filtered and DNA needs to be extracted. (Field work)

2. Extracted DNA is then sent away for sequencing. Further library preparations are done and sequencing is performed. If you would like to understand the sequencing procedure you can have a look at this [Video](https://www.youtube.com/watch?v=fCd6B5HRaZ8), which shows you the Illumina sequencing by synthesis. (Wet Lab)

3. After sequencing you will receive your reads. Your reads are small gene fragments from all the genomes present in your environment. Basically, you now have many puzzles mixed together and now our goal will be to sort the different puzzles apart and then put each puzzle back together.

Steps 1-3 were done before, now we are coming to the steps, which are important for you and your work.

4. We are now coming to the actual bioinformatic analyses. To analyze metagenomes several steps are required:
 - Quality check and trimming
 - Assembly
 - Binning
 - Annotation

  To further improve the quality and completeness of your metagenomic reads you can perform Bin targeted reassemblies. This means you use your retrieved bins and map these back to the assembly. This might fill gaps and lengthen sequences, 


<p align="center">
  <img height="500" src="https://github.com/mmaeke/Metagenomics_Tutorial/blob/master/Images/Metagenomics%20Workflow.png" />
</p>





## Quality check and trimming
When receiving your raw reads after sequencing you very often can see some bias in the beginning of your sequences, also some adapters might still be included in your sequence. A quality check will give you further information about your raw sequences. This check then also helps you to examine the quality of your reads and tells you about contamination. After this first quality check you will then need to trim your sequences accordingly. While trimming, you remove adapters and sequences of bad quality. To see if your trimming worked, you can then repeat the quality check once again after your trimming step.

### FastQC
is one of the programs you can use for the Quality Check. After running this program you will be looking at different modules, which will give you information about your forward and reverse sequencing reads.

1. Basic statistics
2. Per base sequence quality
3. Per sequence quality scores
4. Per base sequence content
5. Per base GC content
6. Per sequence GC content
7. Per base N content
8. Sequence length distribution
9. Sequence Duplication Levels
10. Overrepresented Sequences

You will directly receive information about your different modules. The tick shows you that everything is okay, the exclamation mark tells you something is unusual and you should have a look at it, the X tells you something is really unusual and may be wrong.

A good introduction to the program [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) is given in this [Video](https://www.youtube.com/watch?v=bz93ReOv87Y)

Here is also a brief summary of the different modules:

1. Your basic statistics show you the total number of sequences, Sequence lengths as single number or range and the overall GC % of the library.

2. Per base sequence quality shows you the base calls on the x-axis and the quality score on the y-axis. You are generally looking for quality scores, which are high. Good quality base calls are usually above 20. This plot gives you information about where you should trim your reads.

3. Per sequence quality scores give you information about the distribution of your good sequences. You are generally looking for a high peak on the right side of your x-axis.

4. Per base sequence content should give you an even distribution of the four bases, which do not change with base position. You are looking for parallel lines.

5. Per base GC content

6. Per sequence GC content is plotting the distribution of GC contents across all sequences. Smooth peek with one or two spikes coming out stands for a contamination in your library.

7. Per base N content shows you if there are uncalled bases in your library.

8. Length distribution gives you information if all your sequences are the same length.

9. Sequence duplication level shows how unique your sequences are in the library. So in the best case most sequences occur once. In the top you can see the sequence duplication level, giving you information about the percentage of sequences, which is non unique.

10. Overrepresented sequences looks for individual sequences, which are overrepresented and make up more than 0.1 % of your library. 


## Optional: Coverage, Diversity and similarity of metagenomic samples

- [Nonpareil](http://enve-omics.ce.gatech.edu/nonpareil/): a redundancy-based approach to assess the level of coverage in metagenomic datasets
- [Mash](): R (vegan), Pairwise distances, ordination plots 



## Optional: Abundance estimation of different taxonomic levels within your reads
### Kraken2/Bracken


## Optional: Reference guided assembly

## De novo Assembly
An assembly is a set of sequences which best approximate the original sequenced material. When doing your de novo assembly the program you use looks for overlapping regions on your reads to create longer contigs. From these contigs scaffolds are build. Mostly de Bruijn graphs are used to get the best possible sequence based on kmers. 
### Megahit



## Readmapping
Is used to generate statistics of your assembly.
### Bowtie2

## Binning
### Anvi'o

After binning you can use CheckM to get your Bin statistics.

## Bin targeted reassemblies
To improve your assembly you can map your retrieved bin back to your reads.
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
