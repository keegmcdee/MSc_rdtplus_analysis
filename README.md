# MSc_rdtplus_analysis

Instructions for Jing to begin ICP3 Analysis

Requirements:
- minimap2 installed
- samtools installed
- Download ICP3 Genome
- Find path to RDT+ directory ( /mfs/rdtplus/00_reads/)

Sample Script for running minimap in parallel:
Create a empty directory to use this script in!

```
#!/bin/bash
#Minimap2 script to map rdt+ reads to reference genome ICP3
#KJM May 25 2026

parallel --eta -S 4/SP31,4/SP32,6/SP63,6/SP64,12/SP2000,24/SP5000 --load 80% --plus '
        /mfs/kmac/bin/minimap2 -t 4 -ax map-ont \
        /mfs/path/to/ICP3_genome {} | \
        /mfs/kmac/bin/samtools view -b | \
        /mfs/kmac/bin/samtools sort --write-index -o {/..}.bam
' ::: /mfs/rdtplus/00_reads/*.fastq.gz

```
