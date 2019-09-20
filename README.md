wgs_competency
================

This repository provides functionality for creation of quantitative and graphical reports (see example reports) summarizing a bacterial whole genome DNA sequencing competency assessment analysis pipeline. The included templates may serve as the basis for customization.

The intention is for a user to construct a bioinformatic workflow which produces the required metrics documented in input_file_formatting.txt. The files seq_stats.tsv and run_stats.tsv are comprised of summary stats derived from a distribution of metrics for six isolates sequenced during the 2018 Gen-FS (PulseNet/GenomeTrakr) harmonized Proficiency Testing (PT) exercise as part of a 16-sample 2X250 Illumina MiSeq run (V2 chemistry) using the Nextera XT DNA Library Prep Kit. If the user intends to employ the provided summary stats files, equivalent laboratory SOPs and bioinformatics software should be employed for sequencing and analysis of the isolates listed below. 

## Software Dependencies

#### R:
    3.4 or higher
    
#### R libraries:
    cowplot
    ggplot2
    ggsci
    grid
    gridExtra
    optparse
    xtable

## Usage

In order to create a graphical report -  (first expand the coverage_files archive) 

    create_competency_report.sh -p <prefix> -t <Report title> -T graphical_report_template.Rnw

In order to create a quantitative report - 

    create_competency_report.sh -q -p <prefix> -t <Report title> -T quantitative_report_template.Rnw

## Bacterial Isolates

    We plan to make these isolates available at the [ATCC](https://www.atcc.org/) in the near future. In the meantime, please contact the Maintainer with questions regarding obtaining the isolates.

    SAP18-0432    Salmonella enterica subsp. enterica serovar Enteritidis
    SAP18-H9654   Salmonella enterica subsp. enterica serovar Enteritidis
    SAP18-6199    Salmonella enterica subsp. enterica serovar Typhimurium
    SAP18-8729    Salmonella enterica subsp. enterica serovar Newport
    LMP18-H2446   Listeria monocytogenes
    LMP18-H8393   Listeria monocytogenes

## Reference Genomes and Sequence Data

    Closed reference genomes and a large amount of sequence data from the 2018 Gen-FS PT exercise has been made publicly available at the [NCBI BioProject PRJNA507264](https://www.ncbi.nlm.nih.gov/bioproject/507264 "BioProject PRJNA507264"). The complete sequencing dataset and a journal announcement describing the dataset will be available in the near future. 

## Analysis Software
  If the provided summary stats are used, it is recommended to perform analysis using equivalent versions of the following software programs. 

    CFSAN SNP Pipeline v1.0
        bowtie2 v2.3.4.1-beta
        picard v2.9.2
        samtools v1.3.1
        VarScan v2.3
    FastQC v0.11.5
    samtools v1.3.1
    SPAdes Genome Assembler v3.11.1
    QUAST v4.5

## Metrics
  Definition and derivation of the relevant sequencing metrics (seq_results.tsv, seq_stats.tsv).

    CFSAN SNP Pipeline v1.0
        Reads - the number of sequencing read pairs.
        PercMapped (Reads Mapped)- the percentage of reads which are mappable to the reference.
        MeanDepth - the mean depth of coverage after mapping reads to the reference. 
        SNPs - the number of SNPs reported.
        MeanInsert - the mean length of the sequence between the adapters.
    FastQC v0.11.5
        MeanR1Qual - the mean of the mean read quality scores - forward reads (R1)
        MeanR2Qual - the mean of the mean read quality scores - reverse reads (R2)
    samtools v1.3.1
        CovLT10 (Low Coverage Positions)- the number of positions with depth of coverage < 10X.
        Coverage plots - visualizations of coverage depth and variance across each genomic position.
    SPAdes Genome Assembler v3.11.1 / QUAST v4.5
        NG50 - The N50 assembly quality metric, normalized by genome size. The contig length such that using equal or longer length produces x% of the length of the reference genome, allowing for comparisons between different genomes. 
        Contigs - the total number of contigs in the assembly (> 0 bp).
        GenomeFraction - the percentage of reference to which at least one contig is mappable.
        LengthDelta - the difference between the total length of the assembly (> 0 bp) and the reference length.
        UnalignedLength - the total length of all assembled contigs which could not be aligned to the reference. 
            
  Definition and derivation of the relevant run metrics (run_results.tsv, run_stats.tsv). 
  
    Illumina Sequencing Analysis Viewer (SAV) or BaseSpace or InterOp v1.1.4
        ClusterDensity - the density of clusters for each tile.
        PerClustersPF - the percentage of clusters passing filter for each tile.
        ReadsPF_M - the number of reads/clusters passing filter (Millions).
        TotalYield_GB - the total yield (Gb).
        PerGtQ30 - the percentage of bases with a Q score >= 30.
        PerReadsIdentified - the percentage of ReadsPF_M which were assigned to an index.
        IndexingCV - the coefficient of variation for the number of counts across all indices.

## Authors

Joseph D. Baugher, Ph.D.

## Maintainer

Joseph D. Baugher, Ph.D.
