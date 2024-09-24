# This is tutorial for genome assembly using Flye
Environment management with module system

Here, we'll again use the module system to load the software we want to use.
You need to do this every time you log into the server.

```
$ source /usr/local/ngseq/etc/lmod_profile
```

To check which modules (software) are available, type the following.

Use arrow keys to navigate and type q to exit.

```
$ module avail
```
## Make project directory

Start from your directory on the server for the course and make a new folder for this exercise:

```bash
$ ssh your_BFabric_account_name@fgcz-c-047.uzh.ch
@fgcz-genomics.uzh.ch's password:

$ ssh fgcz-kl-003

$ cd /scratch/bio373_2024/YOUR_NAME
$ mkdir denovo_assembly
$ mkdir denovo_assembly/raw_data
$ mkdir denovo_assembly/flye

```

## Set up input by creating symlinks to input files
We use symlinks to help save diskspace on the server.

```bash
$ cd denovo_assembly/raw_data
$ dataDir="/scratch/bio373_2024/data/denovo_assembly/raw_data"
$ ln -s ${dataDir}/5173_E.hifi_reads_20_perc.fastq
```


## Flye assembler

```
#!/bin/bash
source /usr/local/ngseq/etc/lmod_profile
module load Assembly/Flye/2.8.2

input=/scratch/bio373_2024/YOUR_NAME/denovo_assembly/raw_data/5173_E.hifi_reads.fastq.gz
out=/scratch/bio373_2024/YOUR_NAME/denovo_assembly/flye

flye --pacbio-hifi $input --out-dir $out --genome-size 125m --threads 4 --iterations 3 --keep-haplotypes

```

This takes about 2h.

# Quality assessment 
## Quast
$ source /usr/local/ngseq/etc/lmod_profile 
$ module avail
$ module load QC/QUAST/5.2.0

$ mkdir quast

$ nohup quast.py ./GENOME.fasta -o ./quast -t 2 -e &

## compare the quality of this file with the genome that is assembled using all of the redas








