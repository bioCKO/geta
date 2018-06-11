#GETA
============
GETA is an automatic genome-wide annotation tool (GWAT) with improved accuracy and gene integrity for eukaryotes written by Lianfu Chen, Congcong Liu, Lei Deng and so on.

Introduction
============
GETA can integrate the various evidence from ab initio gene finding and experimental data, including homologous proteins and RNA-Seq data.

GETA is a multi-threaded, automatic, and memory-saving GWAT, which effectively improved the accuracy and completeness of predicted annotation. The current version is v1.0 and later version will support more types of data like the single-molecular sequencing data and add other analysis modules on the basis of continuous improvement in accuracy and completeness.

Installation
============
1.unpack

2.install dependencies:

    ParaFly
    java 1.8.0_144
    HISAT2 2.1.0
    samtools 1.3.1
    hmmer 3.1b2
    Augustus

3.add these directories of the executables to the PATH environment variable

Usage of the main script geta.pl
=================
    Usage:
        geta.pl [options]

    For example:

        geta.pl --RM_species Embryophyta --genome genome.fasta -1 liba.1.fq.gz,libb.1.fq.gz -2 liba.2.fq.gz,libb.2.fq.gz --protein homolog.fasta --augustus_species oryza_sativa_20171120 --out_prefix out --config conf.txt --cpu 80 --gene_prefix OS01Gene --pfam_db /opt/biosoft/hmmer-3.1b2/Pfam-AB.hmm

    Parameters:
    [required]
        --RM_species <string>
        species identifier for RepeatMasker.

        --genome <string>
        genome file in fasta format.

        -1 <string> -2 <string>
        fastq format files contain of paired-end RNA-seq data. if you have data come from multi librarys, input multi fastq files separated by comma. the compress file format .gz also can be accepted.

        -S <string>
        fastq format file contains of single-end RNA-seq data. if you have data come from multi librarys, input multi fastq files separated by comma. the compress file format .gz also can be accepted.

        --protein <string>
        homologous protein sequences (derived from multiple species would be recommended) file in fasta format.

        --augustus_species <string>
        species identifier for Augustus. the relative hmm files of augustus training will be created with this prefix.

    [other]
        --out_prefix <string>    default: out
        the prefix of outputs.

        --config <string>    default: None
        Input a file containing the parameters of several main programs (such as trimmomatic, hisat2 and augustus) during the pipeline. If you do not input this file, the default parameters should be suitable for most situation.
    
        --RM_lib <string>    default: None
        A fasta file of repeat sequences. Generally to be the result of RepeatModeler. If not set, RepeatModeler will be used for producing this file automaticly, which shall time-consuming.

        --cpu <int>    default: 4
        the number of threads.

        --strand_specific    default: False
        enable the ability of analysing the strand-specific information provided by the tag "XS" from SAM format alignments. If this parameter was set, the paramter "--rna-strandness" of hisat2 should be set to "RF" usually.

        --pfam_db <string>    default: None
        the absolute path of Pfam database which was used for filtering of false positive gene models.

        --gene_prefix <string>    default: gene
        the prefix of gene id shown in output file.

        --no_augustus_training_iteration    default: False

    This script was tested on CentOS 6.8 with such softwares can be run directly in terminal:
    1. ParaFly
    2. java version "1.8.0_144"
    3. HISAT2 version 2.1.0
    4. samtools Version: 1.3.1
    5. hmmer-3.1b2
    6. NCBI-Blast+
    7. RepeatMasker
    8. RepeatModeler
    9. genewise

    Version: 2.4.0

Test of GETA
============
we have compared the accuracy of GETA with other methods according to several species. the command line and output GFF3 files can be found at website: <a href="http://122.205.95.116/geta/" target="_noblank">122.205.95.116/geta/</a>
