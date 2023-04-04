---
layout: page
title: Translate First ORF
description: "Translate first ORF of feach DNA sequence into a protein sequence<br><b>Using: </b><em>Python, pytest</em>"
img: 
importance: 5
category: work
---

<em>Author:</em> Inbar Ofer

- Access to the GitHub repository may be provided upon request.

## Overview

This program takes a FASTA file of DNA sequences, transcribes them into RNA sequences, finds the first open-reading frame (ORF) for each sequence, and translates it into a protein sequence. The output is printed to the console as the record ID and its translated first ORF separated by a tab space.

## Running translate_first_orf.py

This program is run from the command line, but there are multiple ways to do so. Once within the assignment directory, the program can be run in the following ways:
* ```./translate_first_orf.py [FASTA file]```
* ```python3 translate_first_orf.py [FASTA file]```

An example of how to run ```translate_first_orf``` with the file ```dmel-all-chromosome-r6.17.fasta``` provided in class is as follows:

```./translate_first_orf.py dmel-all-chromosome-r6.17.fasta```

Output:
```
2L:     MHDRGSRTDI*
2R:     MSF*
3L:     MIAYARVVPTYCAL*
3R:     MGPSTEPSTEPSTGPVRDQYGTSTGPVRDQYGTSTGPVRDQYGTSTGPVRDQYGTSTGPSTEPSTGPVRDQYGTSTGPVRD*
4:      MNGIIIGNSTIFNNLYQSTNLVNALLIYLT*
```