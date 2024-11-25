# Part 2: Bacterial genome assembly
The goal of the second part of this practical is to assemble a bacterial genome using sequencing reads. The genome will be assembled using short-read sequencing data to produce '**contigs**'. **Contigs** is a term that means contiguous DNA and refers to the consensus sequence that is formed when sequencing reads (usually from fastq files) are ‘stitched together’ to form regions of the genome. With short reads, repetitive sequences usually prevent complete closed genomes from being produced and instead the end result is usually smaller pieces of contiguous DNA that make up most of the genome. Hybrid assembly approaches (i.e. using long and short read sequencing data together) can be used to try and 'close the genome', to give you a complete genome where you know how everything fits together. For this practical we will be working with short reads only, obtained from illumina sequencing of a *Pseudomonas aeruginosa* genome.

## **TABLE OF CONTENTS**
- [2.1 Manage data](#21-Manage-data)
- [2.2 Running fastQC](#22-Running-fastQC)
- [2.3 Genome assembly](#23-Genome-assembly)
- [2.4 Species identity check](#24-Species-identity-check)
- [2.5 Extra - further data analysis](#25-Extra---further-data-analysis)

*Pseudomonas aeruginosa* is a Gram-negative bacterium and opportunistic pathogen. It is a major problem in clinical settings and is as a major caustive pathogen of ventilator-associated pneumonia. *P. aeruginosa* is becoming increasingly resistant to the antibiotics we use to treat it. Genome sequencing data is useful for understanding what the population of *P. aeruginosa* looks like, how many acquired antibiotic resistance genes this pathogen carries, and understanding how *P. aeruginosa* is evolving in clinically relevant environments (such as within ICU patients with pneumonia infections).

## 2.1 Manage data

Let's first create a new directory (within our intro folder) to work in:

:pencil2:**code:**
```bash
mkdir assembly
cd assembly
```

Check you are now in your new folder.

For the purposes of this practical, we will be using a pair of forward and reverse fastq.gz (comparessed gzipped fastq) files from *P. aeruginosa* available from the European Nucleotide Archive. 
You can download this data using the command wget followed by the address to that file(s)

:pencil2:**code:**
```bash
wget ftp.sra.ebi.ac.uk/vol1/run/ERR549/ERR5490552/PSA-2017-01_1.fastq.gz
```

However, all the data needed for the first week of this course is already available in DTC computer in the followed location

```bash
/usr/local/bioinformatics
```
If you navigate to this location you will see four folders, one for each practical. 

If you are working in your own computer / VM follow the next steps to get the pair of reads:


:pencil2:**code:**
```bash
wget ftp.sra.ebi.ac.uk/vol1/run/ERR549/ERR5490552/PSA-2017-01_1.fastq.gz
wget ftp.sra.ebi.ac.uk/vol1/run/ERR549/ERR5490552/PSA-2017-01_2.fastq.gz
```

To check that the files have downloaded we can use the **ls -lh** command (**-l** long; **-h** human-readable), which also allows us to check the size of the files:

:pencil2:**code:**
```bash
ls -lh
```

The files that we've downloaded are gzipped **FASTQ** files. Take a look at one of them:

```bash
PSA-2017-01_1.fastq.gz
PSA-2017-01_2.fastq.gz
```

We can use a combination of commands to view the first few lines of a compressed files. 

```bash
zcat /usr/local/bioinformatics/1-intro/PSA-2017-01_1.fastq.gz | head -n 20
```
**zcat** decompress the file and shows it in the terminal. However, **fastq** files contained millions of reads, and we want to avoid “seing” the whole file in the terminal. In order to avoid this, we add another command, in this case head, after the symbol | which pipes the output zcat as an input of the next command head -n 20. In the end, you’ll see only the first 20 lines of the fastq.gz file. 

How does it look like commpare to a fasta file?

## 2.2 Running fastQC
The tool **fastqc** assesses the quality scores across all of the reads in your data. You can read more about it here: https://dnacore.missouri.edu/PDF/FastQC_Manual.pdf
First, create a folder to save fastqc results

:pencil2:**code:**
```bash
mkdir fq-results
```

Let’s run fastqc on our 2 samples:

:pencil2:**code:**
```bash
fastqc /usr/local/bioinformatics/1-intro/PSA-2017-01_1.fastq.gz -o fq-results
fastqc /usr/local/bioinformatics/1-intro/PSA-2017-01_2.fastq.gz -o fq-results
```

**-o**: output directory. Location where the files will save.

View the files that have been generated:

:pencil2:**code:**
```bash
cd fq-results
ls *fastqc*
```

:rocket:**Output:**
```bash
PSA-2017-01_1.fastqc.html
PSA-2017-01_1.fastqc.zip
PSA-2017-01_2.fastq.html
PSA-2017-01_2.fastq.zip
```

For each file, **fastQC** has produced both a .zip archive containing all the plots, and a html report. We can open the html files using a web browser: e.g.:

:pencil2:**code:**
```bash
google-chrome PSA-2017-01_1.fastqc.html&
```

For each position, a boxplot is drawn with:

• the median value, represented by the central red line

• the inter-quartile range (25-75%), represented by the yellow box

• the 10% and 90% values in the upper and lower whiskers

• the mean quality, represented by the blue line

The y-axis shows the quality scores. The higher the score, the better the base call. The background of the graph divides the y-axis into very good quality scores (green), scores of reasonable quality (orange), and reads of poor quality (red). It is normal with all Illumina sequencers for the median quality score to start lower over the first 5-7 bases and to then rise. The quality of reads on most platforms will drop at the end of the read. This is often due to signal decay or phasing during the sequencing run. We can see that our sequence length is 35-250bp. This makes sense, because this was sequenced with a 250 bp paired-end sequencing run on an Illumina MiSeq sequencer. The sequencing reads have a %GC of 65, this is within the expected
%GC range for Pseudomonas aeruginosa (which has a highly GC biased genome). Anything above a score of 25 is usually considered good quality, so we can see these are reasonable quality reads.
Check the fastqc reports for both files, which file is of better quality?


**Optional step: trimming & filtering data**
Low quality sequences and adapters can be removed used programs such as trimmomatic (read more here: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4103590/ , https://www.melbournebioinformatics.org.au/tutorials/tutorials/assembly/assembly- protocol/).
Whether you should do this can depend on the objective of your sequencing experiments (e.g. read more here: https://dnatech.genomecenter.ucdavis.edu/faqs/when-should-i- trim-my-illumina-reads-and-how-should-i-do-it/).
We will not do this today, but you should be aware of it for genome assemblies in the future.

## 2.3 Genome assembly
**SPAdes** is one of a number of de novo assemblers that uses short read sets as input (e.g. Illumina Reads). When a genome is sequenced, it is fragmented into lots of short sequencing fragments called ‘**reads**’. Assembling the genome means putting the pieces back together. The assembly method **SPAdes** uses is based on de Bruijn graphs, which you can read about on wikipedia: they use overlaps between reads to build up the genome.
So in simple words, assembling a genome means putting together the sequenced random fragments (known as **reads**) into longer sequences (called **contigs**).
The **SPAdes** program has several options (read more here: https://github.com/ablab/spades), which can be listed if you test **spades.py** and press **Enter**. The most basic options to specify are:

- **-1** is input file of forward reads
- **-2** is input file of reverse reads
- **-o** is the output directory

As a pipeline, SPAdes will perform both a read error corection step and then an assembler step. Automatically, it will perform both. But you can also get it to run just one by using:

- **--only-error-correction** [Performs read error correction only]
- **--only-assembler** [Runs assembly module only]

For the sake of time, we are going to run **SPAdes** in assembler mode only (running both would take >1 hour). This will likely effect the downstream quality of our genome (e.g. a higher number of contigs!), so is not something you would generally want to do, but will allow us to produce assembled genomes which we can continue the practical with.

To run **SPAdes** to assemble our paired fastq reads PSA-2017-01_1.fastq.gz and PSA-2017-01_2.fastq.gz in assembly mode only:

:pencil2:**code:**
```bash
spades.py -1 [location-to-read-1] -2 [location-to-read-2] –-only-assembler -o spades_assembly
```

replace the information in [ ] to the path of each fastq file. Wait for the command to run. **SPAdes** should give some output about what it is doing. At the end, you might see an assembly warning about erroneous kmer, that is OK for the sake of this exercise (re. run in assembly mode only).

Navigate into your spades_assembly output folder and check whats there:

:pencil2:**code:**
```bash
cd spades_assembly
```

The file '*contigs.fasta*' is the contig file produced from the reads, and what we will be working with. You can read more about what the other files are on the GitHub page: https://github.com/ablab/spades

#
Exercice
How many contigs (sequences) have the result of the assembly (*contigs.fasta*)  
#

We can run *QUAST* (QUality ASsessment Tool) for an overview of our assembly metrics. You can read more about QUAST here: https://quast.sourceforge.net/docs/manual.html:

:pencil2:**code:**
```bash
quast.py contigs.fasta
```

After it has finished running, you should see a new folder with the results in has been created - '**quast_results**'.

Navigate into this folder, and then into the new results (**results_data_hour**) sub-folder. In this folder use '**ls**' to check what is there. We are interested in the '**report.txt**' file, which is a summary report file.

To see the contents, we can use the **vi editor** or **cat**:

:pencil2:**code:**
```bash
cat report.txt
```

Looking at this report we can see there are a total of 864 contigs with a size of >= 1000bp. The total length is ~6.56Mb, which is within the size range we expect for a *P. aeruginosa* genome (5.5Mb - 7Mb). The GC is ~66%, which again is within the GC range we expect for a *P. aeruginosa genome*. The largest contig is ~47,000bp.

## 2.4 Species identity check
A final step in our genome quality check is to confirm that the genome and the DNA it is composed of belongs to our species of interest and that it isn’t contaminated with DNA from another bacterium. There are a number of tools that can do this and this depends on whether you want to check your data before it has been assembled using software such as **KRAKEN** or after it has been assembled using tools such as **MASH**. We will query our assembled genome against a reference database called **rMLST** available on the online, publicly available website https://pubmlst.org/species-id.

Species identification in **rMLST** uses genes involved in the ribosome machinery which are core to all bacteria and for which sequence variations are associated with specific bacterial species. You can query your data by directly uploading your **contigs.fasta** file to the database via the webserver.

Search '**identify species pubmlst**' using google or (https://pubmlst.org/bigsdb? db=pubmlst_rmlst_seqdef_kiosk)
Once you have navigated to this page, click in the '**select FASTA file**' box, navigate to where the **SPAdes** assembled 'contigs.fasta' file is and select this file, then click
**Submit**.

Your sequence data will be compared against all of the >400,000 genomes present in the **rMLST** database to see how closely it matches in its ribosome sequences to ones defined in the database.
Does the output match your expectations? (*Pseudomonas aeruginosa*)

## 2.5 Extra - further data analysis
Here is an (optional) data analysis exercise you can try to explore your assembled genome:

1. Does your assembled genome contain any acquired antibiotic resistance genes? (hint: try finding some antibiotic resistance gene databases and blasting these gene fasta sequences against your genome using blastn in command line)
**Blast** (command line version) has been installed on the computers + virtual machines (read more here: https://www.ncbi.nlm.nih.gov/books/NBK279690/)
As with the webserver, you can run **blastn** queries against a database (quick start here: https://www.ncbi.nlm.nih.gov/books/NBK569856/) or against another file.
To list these options available:

:pencil2:**code:**
```bash
blastn -help
```

A basic quickstart on how to query one file (e.g. an antibiotic resistance gene) against another (e.g. a genome):

:pencil2:**code:**
```bash
blastn -query queryfilename.fasta – subject subjectfilename.fasta -out outputfilename.txt
```

You can specify search options, e.g. "-perc_identity 95 -qcov_hsp_perc 95 - num_alignments 1".
