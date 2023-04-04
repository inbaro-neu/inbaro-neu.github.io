---
layout: page
title: Transcriptome Assembly
description: "Automate guided and de novo transcriptome assembly<br><b>Using: </b><em>bash, Trinity, Slurm</em>"
img: 
importance: 4
category: work
---

<em>Author:</em> Inbar Ofer

- Access to the GitHub repository may be provided upon request.

## Overview

This program is a bash script designed to automate the guided and de novo transcriptome assembly using Trinity for RNA sequencing data. The script includes Slurm directives for resource allocation, software module loading, working directory setup, and file copying for the analysis.

1. Specify Slurm parameters.
2. Load the necessary software modules and create a log directory.
3. Copy the trimmed fastq data and alignment files to the working directory.
4. Run guided assembly using Trinity by merging all BAM alignment files and assembling the guided transcriptome.
5. Analyze the guided transcriptome and output the stats.
6. Run de novo assembly using Trinity and assemble the de novo transcriptome.
7. Analyze the de novo transcriptome and output the stats.
8. Move the output files to the user's home directory.

## Running sbatch_trinity.sh

```sbatch sbatch_trinity.sh```

## Methods

### mergeAll.sh

This bash script is designed to merge multiple sorted BAM files using the `samtools` [1] program. The merged BAM file can be used for downstream analysis, such as transcriptome assembly.

`samtools` is used with the following parameters:
* `merge`: the subcommand to merge multiple BAM files into a single file.
* `-b data/bam/bamIn.txt`: the `-b` option specifies that the input files are listed in a text file, `bamIn.txt`, which contains the paths to the input files. This option is used to avoid command-line length limits when merging a large number of files.
* `data/bam/bamIn.txt`: the path to the input file that contains the list of sorted BAM files to be merged.
* `data/bam/AipAll.bam`: the output file name of the merged BAM file. The output file is stored in the data/bam directory.

### runTrinity.sh

This bash script is designed to perform a guided assembly using Trinity [2], a de novo transcriptome assembler, with the aid of the genome-aligned RNA-Seq reads in a BAM format.

Trinity is used with the following parameters:
* `--genome_guided_bam data/bam/AipAll.bam`: the path to the BAM file containing the genome-aligned RNA-Seq reads.
* `--genome_guided_max_intron 10000`: the maximum intron length allowed in the genome-guided assembly. In this case, the maximum intron length is set to 10000 bp.
* `--max_memory 10G`: the maximum amount of memory that Trinity can use for the assembly process. In this case, the maximum memory is set to 10 GB.
* `--CPU 4`: the number of CPUs/threads to be used for the assembly process. In this case, 4 CPUs are used.
* `--output results/trinity_guided`: the output directory where the results of the guided assembly will be stored.

### analyzeTrinity.sh

This bash script is designed to generate statistics for the guided transcriptome assembly output by Trinity.

The script runs TrinityStats.pl, a Perl script that generates assembly statistics for Trinity output. The script takes the following input:
* `results/trinity_guided/Trinity-GG.fasta`: the path to the guided transcriptome assembly output by Trinity.

### trinityDeNovo.sh

This bash script is designed to perform a de novo transcriptome assembly using Trinity [2] with the paired-end RNA-Seq reads in FASTQ format.

Trinity is used with the following parameters:
* `--seqType fq`: the type of input sequence data, which in this case is paired-end FASTQ.
* `--output results/trinity_de_novo`: the output directory where the results of the de novo assembly will be stored.
* `--max_memory 10G`: the maximum amount of memory that Trinity can use for the assembly process. In this case, the maximum memory is set to 10 GB.
* `--CPU 4`: the number of CPUs/threads to be used for the assembly process. In this case, 4 CPUs are used.
* `--left $leftReads`: the path to the left reads in FASTQ format. The variable $leftReads contains a list of paths to the left reads that are obtained using the ls command.
* `--right $rightReads`: the path to the right reads in FASTQ format. The variable $rightReads contains a list of paths to the right reads that are obtained using the ls command.

### analyzeTrinityDeNovo.sh

This bash script is designed to generate statistics for the de novo transcriptome assembly output by Trinity.

The script runs TrinityStats.pl, a Perl script that generates assembly statistics for Trinity output. The script takes the following input:
* `results/trinity_de_novo/Trinity.fasta`: the path to the de novo transcriptome assembly output by Trinity.

## Assembly Statistics

The de novo assembly has more Trinity genes and transcripts than the guided assembly, which could indicate that it was able to capture more of the transcriptome. However, the guided assembly may have a more accurate representation of the transcriptome because it was guided by an existing reference genome. The higher N50 value in the guided assembly could indicate a more contiguous assembly, which is generally considered to be an indicator of higher quality.

## References

1. Danecek, P., Bonfield, J. K., Liddle, J., Marshall, J., Ohan, V., Pollard, M. O., Whitwham, A., Keane, T., McCarthy, S. A., Davies, R. M., & Li, H. (2021). Twelve years of SAMtools and BCFtools. _Gigascience_, _10_(2). [https://doi.org/10.1093/gigascience/giab008](https://doi.org/10.1093/gigascience/giab008).

2. Grabherr, M. G., Haas, B. J., Yassour, M., Levin, J. Z., Thompson, D. A., Amit, I., ... & Regev, A. (2011). Full-length transcriptome assembly from RNA-Seq data without a reference genome. _Nature biotechnology_, _29_(7), 644-652. [https://doi.org/10.1038/nbt.1883](https://doi.org/10.1038/nbt.1883).