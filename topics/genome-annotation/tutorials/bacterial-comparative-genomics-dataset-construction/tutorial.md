---
layout: tutorial_hands_on

title: Dataset construction for bacterial comparative genomics
zenodo_link: 'https://zenodo.org/records/1'
draft: true
questions:
- How to build a sound bacterial genome dataset for a comparative analysis
objectives:
- Select all the genome assemblies of a bacterial species
- Retrieve the metadata of these genomes in a table
- Retrieve the DNA sequences and annotated genomes in Galaxy
time_estimation: 1H
key_points:
- The **ncbi-dataset** tool provides facilities to extract genome data and metadata from Genbank and RefSeq repositories
- The **dRep** tool provides facilities to analyze genome diversity in a bacterial genome dataset
- Depending on the dataset features and the scientific question, it is advised to **dereplicate the genome dataset** using adjusted clustering parameters, i.e. select the best quality representative genomes in the dataset and remove the genomes that are nearly identical and do not provide additional valuable genomic content.
contributions:
  authorship:
  - hchiapello
  - bebatut
  - vloux
edam_ontology:
- topic_0622 # Genomics
- topic_3301 # Microbiology
level: Introductory
tags:
- microgalaxy
---

Introduction


> <agenda-title></agenda-title>
>
> In this tutorial, we will cover:
>
> 1. TOC
> {:toc}
>
{: .agenda}

# Get public genomes from NCBI of your favorite bacterial species

> <hands-on-title>Build a table of public genomes of your favorite bacterial species</hands-on-title>
>
> 1. > <hands-on-title> Get genome information at NCBI </hands-on-title>
 - Go the *NCBI datasets web site*: 'https://www.ncbi.nlm.nih.gov/datasets/'
 - Enter the name of you favorite bacterial species in the dark blue frame: here we propose *Streptococcus salivarius* 
- Read carefully the resulting web page and answer questions
>


> <question-title>General information on *S. salivarius* NCBI public genomes</question-title>
>
> 1. What is the NCBI Taxonomy id of *S. salivarius* ?
> 2. How many public genomes are they for *S. salivarius* in NCBI ?
> 3. What is the reference genome accession number of *S. salivarius* ?
>
> > <solution-title></solution-title>
> >
> > 1. *S. salivarius* taxonomy id: 1304
> > 2. 517 public *S. salivarius* genomes (date: 2015/07/24)
> > 3. *S. salivarius* reference genome accession: GCF_000253315.1
> >
> {: .solution}
>
{: .question}


> 2. > <hands-on-title>Create a metadata report for all public genomes of your favorite species</hands-on-title>
>
> 1. Create a new history for this analysis
>
>    {% snippet faqs/galaxy/histories_create_new.md %}
>
> 2. Rename the history
>
>    {% snippet faqs/galaxy/histories_rename.md %}
>
> 3. Use the Tool {% tool [NCBI Datasets Genomes](toolshed.g2.bx.psu.edu/repos/iuc/ncbi_datasets/datasets_download_genome/16.42.0+galaxy0) %} to generate a report of public genomes of your bacetrial species
>     - In *"Query"*:
>        - *"Choose how to find genomes to download"*: `By Taxon (NCBI Taxonomy id, scientific or common name)` and entee the taxon id for *S. salivarius*
>     - In *"Filter and Limit"*: 
>        - set **Assembly source** to RefSeq
>     - In *"Ouput Options"* 
>        - In *"Columns in the report"* add *at least* the following important columns: Asssembly level, Assembly release data, Assembly sequencing tech, Assembly Stats total number of chromosomes, Assembly stats Total Sequence Length, Assembly Stats Contig N50, Assembly Biosample accession number,Assembly Biosample Collection Date, Assembly Biosample geographic location, Assembly Biosample isolation source
>         - In *"Include"* For this first query remove the genomic sequence (genome) to be able to refine your dataset before ddownloading the corresponding genomes


> <question-title>General information on *S. salivarius* NCBI  genome datasets</question-title>
>
> 1. How many RefSeq public genomes are there in the resulting table *S. salivarius* ?
> 2. What is the total sequence length of the reference genome  of *S. salivarius* ?
>
> > <solution-title></solution-title>
> >
> > 1. Number of Refseq *S. salivarius*  genomes: 282 (date: 2015/07/24)
> > 2. The reference genome of S. salivarius has accession number GCF_000253315.1 and has 2.210.574 pb length
> >
> {: .solution}
>
{: .question}

***TODO***: *Add an explanation about why it is better to use only Refseq genomes (quality check+ homogeneous annotatione*

# Extract IDs from NCBI genome data report

> <hands-on-title> Task description </hands-on-title>
>
> 1. {% tool [Cut](Cut1) %} with the following parameters:
>    - *"Cut columns"*: `c1`
>    - {% icon param-file %} *"From"*: `NCBI Genome Datasets: Data Report` (Input dataset)
>
>  2. {% tool [Remove beginning](Remove beginning1) %} with the following parameters:
>    - *"Remove first"*: `1`
>    - {% icon param-file %} *"from"*: `outfile` (output of **Cut** {% icon tool %})
>
>    > <comment-title> short description </comment-title>
>    >
>    > A comment about the tool or something else. This box can also be in the main text
>    {: .comment}
>
{: .hands_on}


# Download genomes from NCBI

> <hands-on-title> Task description </hands-on-title>
>
> 1. {% tool [NCBI Datasets Genomes](toolshed.g2.bx.psu.edu/repos/iuc/ncbi_datasets/datasets_download_genome/16.42.0+galaxy0) %} with the following parameters:
>    - In *"Query"*:
>        - *"Choose how to find genomes to download"*: `By NCBI assembly or BioProject accession`
>            - *"Enter accession or read from file ?"*: `Read a list of NCBI Assembly accessions from a dataset`
>                - {% icon param-file %} *"Select dataset with list of NCBI Assembly accessions"*: `out_file1` (output of **Remove beginning** {% icon tool %})
>     - In *"Ouput Options"* 
>         - In *"Include"* Add the *"Genbank flat file" to the genomic sequence (genome)
>
>    ***TODO***: *Consider adding a comment or tip box*
>
>    > <comment-title> short description </comment-title>
>    >
>    > A comment about the tool or something else. This box can also be in the main text
>    {: .comment}
>
{: .hands_on}

***TODO***: *Consider adding a question to test the learners understanding of the previous exercise*

> <question-title></question-title>
>
> 1. Question1?
> 2. Question2?
>
> > <solution-title></solution-title>
> >
> > 1. Answer for question1
> > 2. Answer for question2
> >
> {: .solution}
>
{: .question}


# Analyze genome diversity in the dataset and optionnaly dereplicate

to do :  dRep compare first with default parameters and dRep derplicate with 1st threshold set to 0.07 (instead of 0.9) and second threshold set to 0.99 (instead of 0.95)

# Conclusion

Sum up the tutorial and the key takeaways here. We encourage adding an overview image of the
pipeline used.