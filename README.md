# MSc_rdtplus_analysis

Instructions for Jing to begin ICP3 Analysis

Requirements:
- minimap2 installed
- samtools installed
- Download ICP3 Genome
- Find path to RDT+ directory ( /mfs/rdtplus/00_reads/)

Sample Script for running minimap in parallel:

```
#!/bin/bash
#Minmap2 script to map rdt+ reads to reference genome ICP3
#KJM May 25 2026

parallel --eta -S 4/SP31,4/SP32,6/SP63,6/SP64,12/SP2000,24/SP5000 --load 80% --plus '
        /mfs/kmac/bin/minimap2 -t 4 -ax map-ont \
        /mfs/path/to/ICP3_genome {} | \
        /mfs/kmac/bin/samtools view -b | \
        /mfs/kmac/bin/samtools sort --write-index -o output_directory/{/..}.bam
' ::: /mfs/kmac/rdtplus/fastqziped/*.fastq.gz

```
```
bash map.sh > ./map_log.txt 2>&1 && echo "mapping completed" > ./mmap_done.log
```
