# FLIRTy

[![Docker CI](https://github.com/William-Gardner-Biotech/FLIRTy/actions/workflows/docker-image.yml/badge.svg)](https://github.com/William-Gardner-Biotech/FLIRTy/actions/workflows/docker-image.yml)

FLIRTy: Finding Loose Interactions and Rogue Targets. Bioinformatic tool to locate which primers are cross reacting in multiplex reactions.

This Nextflow pipeline is designed to identify potential off-target binding sites for primers in a multiplex PCR reaction. By analyzing the sequencing reads and removing reads that map to the intended amplicon regions, the pipeline can identify primers that may bind outside of their intended.

## Overview

The pipeline consists of the following main processes:

1. **MATCH_AMP**: Finds the matching amplicon region for each primer based on the provided primer and amplicon information.
2. **REMOVE_AMP_REGION**: Removes reads that map to the intended amplicon regions, leaving only reads that potentially represent off-target binding sites.
3. **BACK_BLAST**: Performs a BLAST search of the primers against the remaining reads to identify potential off-target binding sites.
4. **BUILD_BLAST_DB**: Builds a BLAST database for each set of remaining reads (after removing the amplicon regions).
5. **PERFORM_BLAST**: Performs a BLAST search of the primers against the corresponding BLAST database to identify potential off-target binding sites.

## Usage

To run the pipeline, you'll need to provide the following input files:

- `primers`: A file containing the primer sequences, in the format `chr\tstart\tend\tprimerName\tprimerSeq`.
- `amplicons`: A BED file containing the amplicon regions.
- `inputBAM`: A BAM file containing the sequencing reads.
- `ref_genome`: The reference genome FASTA file.

You can then run the pipeline using the following command:

```bash
nextflow run main.nf --primers /path/to/primers.txt --amplicons /path/to/amplicons.bed --inputBAM /path/to/input.bam --ref_genome /path/to/ref_genome.fa
