---
layout: page
title: Interleave
description: "Interleave mate-pair FASTQ files<br><b>Using: </b><em>Python, Biopython</em>"
img: 
importance: 5
category: work
---

<em>Author:</em> Inbar Ofer

- Access to the GitHub repository may be provided upon request.

## Overview

This program takes two mate-pair FASTQ files and interleaves them into a single FASTQ file. It uses the Biopython library to read and write FASTQ and FASTA files. Additionally, the program generates a log file that records the progress of the interleaving process, including a summary of the input arguments. The output file and log file paths can be customized using command line arguments.

## Running interleaved.py
This program is run from the command line, but there are multiple ways to do so. Once within the ```/scripts/``` directory, the program can be run in the following ways:
* ```./interleaved.py --pathInputR1 [Left FASTQ file] --pathInputR2 [Right FASTQ file]```
* ```python3 interleaved.py --pathInputR1 [Left FASTQ file] --pathInputR2 [Right FASTQ file]```

Here are some optional arguments:
* ```-o``` and ```--output``` specify the output file path (default is ```../data/{currentDateTime}.interleaved.fasta```)
* ```--logFolder``` specifies the log file path (default is ```../results/logs/```)
* ```--logBase``` specifies the base name of the log file (default is ```interleaved.py```)
* ```-h``` and ```--help``` show a help message with a description of the program and its arguments

## Example
For example, running
```
python3 interleaved.py --pathInputR1 ../data/top24_Aip02.R1.fastq --pathInputR2 ../data/top24_Aip02.R1.fastq -o Aip02.interleaved.fasta
```
will create a new FASTA file called ```Aip02.interleaved.fasta``` in the ```../results/interleaved``` directory. The log file will be created in the ```../results/logs/``` directory and will be named ```{currentDateTime}_interleaved.py.log```.