---
layout: page
title: Analyze Genome Assembly
description: "Analyze genome assembly from NGS reads<br><b>Using: </b><em>bash, Trimmomatic, SPAdes, Quast</em>"
img: 
importance: 4
category: work
---

<em>Author:</em> Inbar Ofer

- Access to the GitHub repository may be provided upon request.

## Overview

This program performs an analysis of a genome assembly from next-generation sequencing (NGS) reads. The sbatch_assembleGenome.conf is currently configured to assemble the <i>Rhodobacter spheroides</i> genome, with the SRA accession number of SRR522244.

## Running sbatch_assembleGenome.sh
This program is run from the command line, but first you must load the Anaconda environment for BINF6308:
```
module load anaconda3/2021.11
source activate "BINF-12-2021"
```
Then, you can run the program by typing the following command:
```./sbatch_assembleGenome.sh```.

Alternatively, you can run the program by running each of the scripts individually:
1. ```source sbatch_assembleGenome.conf``` in order to set the environment variables
2. ```srun --partition=short --pty --export=ALL --nodes=1 --ntasks=1 --mem=10Gb --time=04:00:00 /bin/bash``` in order to request a compute node on the Discovery remote server
3. ```./getNGS.sh```
4. ```./trim.sh```
5. ```./runSpades.sh```
6. ```./runQuast.sh```

## Methods
The program uses the following scripts to assemble the genome:

### 1. getNGS.sh
This program downloads the raw NGS data from the NCBI SRA database using fasterq-dump.

fasterq-dump is used to convert SRA files into the more commonly used FASTQ format, which is a widely accepted format for storing raw sequence data with associated quality scores. The command works faster than the original fastq-dump command provided in earlier versions of the SRA Toolkit.

getNGS.sh uses the following flags/options with fasterq-dump:
* ```--split-3 ${SRR_ID}```: split the reads into two files, one for each end of the read
* ```-O "../data/untrimmed"```: output the files to the untrimmed directory

### 2. trim.sh
This program trims the raw NGS data using Trimmomatic, a widely used, flexible, and high-performance command-line Java-based tool designed to identify and remove low-quality bases, adapter sequences, and other technical artifacts that can negatively affect downstream analysis of sequencing data.

trim.sh uses the following flags/options with Trimmomatic:
* ```PE``` indicates that the input is paired-end (reads).
* ```-threads 1``` indicates that the program should use 1 thread.
* ```-phred33``` indicates that the quality scores are encoded using ASCII+33.
* The next two parameters are the left and right read files, respectively.
* The next four parameters are the output files for paired and unpaired output. The unpaired output files contain reads where the mate was deleted due to overall low quality. Since you always have to have the same number of reads in the left file and right file for paired-end reads, if one read is deleted entirely due to low quality, its mate has to be deleted as well. The reads whose mates have been deleted end up in the unpaired files.
* ```HEADCROP:0``` indicates that the none of the first bases of each read should be removed.
* ```ILLUMINACLIP:$PATH_TO_TRIMMOMATIC/adapters/TruSeq3-PE.fa:2:30:10``` indicates that the TruSeq3-PE.fa file should be used to remove adapters. The first number indicates the maximum mismatch count which will still allow a full match to be performed. The second number indicates the minimum score of the match between any adapter and the read. The third number indicates that if a full match is not found, the algorithm will check for a partial match with the next lowest score. If the score is higher than the second number, the match will be performed. The second and third numbers are there to prevent the algorithm from removing parts of the read that happen to match the adapter.
* ```LEADING:20``` indicates that any base with a quality score less than 20 should be removed from the beginning of the read.
* ```TRAILING:20``` indicates that any base with a quality score less than 20 should be removed from the end of the read.
* ```SLIDINGWINDOW:4:30``` indicates that any window of 4 consecutive bases where the average quality score is less than 30 should be removed.
* ```MINLEN:36``` indicates that any read that is less than 36 bases long should be removed.
  
### 3. runSpades.sh
This program assembles the genome using SPAdes (St. Petersburg genome assembler) and the trimmed, paired reads extracted using getNGS.sh and trim.sh. SPAdes is a widely used, open-source genome assembly tool designed for de novo assembly of small genomes, such as bacteria, fungi, and viruses, using high-throughput sequencing data.

runSpades.sh uses the following flags/options with SPAdes:
* ```-1``` indicates the first read file that should be used.
* ```-2``` indicates the second read file that should be used.
* ```-o``` indicates the output directory for the assembly results.

### 4. runQuast.sh
This program runs Quast to evaluate the assembly. QUAST (Quality Assessment Tool for Genome Assemblies) is an open-source, user-friendly tool designed to evaluate and provide statistics for genome assemblies. QUAST generates a comprehensive report that includes various assembly metrics, such as N50 and L50 statistics, total length, and number of contigs.

runQuast.sh uses the following flags/options with Quast:
* The first parameter is the reference genome.
* ```-o``` indicates the output directory.

## Conclusions from Analysis

<b>Download Quast report: </b><a href="/assets/pdf/quast_report.pdf" target="_blank" rel="noopener noreferrer"><i class="fas fa-file-pdf" style="font-size: 1.5rem"></i></a>

<b>What were the key metrics?</b>

The key metrics from the Quast report were:
* N50: 25,496
* L50: 51
* Number of contigs: 323
* Total length: 4,531,150

<b>How "good" was the assembly?</b>

The N50 value is a popular way to guage an assembly's quality. In simple terms, it's the length of the shortest contig in a set where the fewest (biggest) contigs make up at least half of the assembly. When the N50 value is higher, it's usually a good sign because it means the contigs are longer and the assembly is more contiguous.

The L50 value counts the contigs that, when added together, make up at least half of the assembly. If the L50 value is lower, it's generally better because it means fewer contigs are needed to cover half of the assembly.

With an N50 value of 25,496 and an L50 value of 51, this assembly seems pretty contiguous, with a decent amount of longer contigs. However, there is still room for improvement, as an even higher N50 value and a lower L50 value would mean an even more contiguous assembly.

Another way to gauge the assembly's quality is by looking at the number of contigs and the total length of the assembly. Ideally, you want a smaller number of contigs and a total length close to the anticipated genome size.

The assembly's contig count (323) is relatively low, which is a positive sign because it means the genome is represented by fewer, longer segments.

<i>Rhodobacter sphaeroides</i>, the bacterium in question, has a genome size of around 4.6 million base pairs. So, since the total length of the assembly is close to that, it's a good indicator that the assembly likely covers most, if not all, of the genome.

Overall, this assembly seems to be of reasonable quality, with a total length near the expected genome size and a fairly low number of contigs. However, there's still a bit of room for improvement when it comes to contiguity, as the N50 and L50 values suggest.