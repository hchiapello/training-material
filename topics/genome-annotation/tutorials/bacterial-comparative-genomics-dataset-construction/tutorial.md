---
layout: tutorial_hands_on

title: Public dataset construction for bacterial comparative genomics
zenodo_link: 'https://zenodo.org/records/1'
draft: true
questions:
- How to can a sound bacterial genome dataset be built for a comparative analysis ?
- How can publicly available assemblies be listed, filtered and downloaded in different formats ?
- How can genome diversity within this dataset be evaluated ?
- How to perform dereplication on a large dataset, i.e. identify "identitical" genomes and reduce the dataset by selecting the highest quality representative genome in each replicate set?
objectives:
- Retrieve the publicly available genome assemblies of a bacterial taxon (usually a species or genus)
- Retrieve the corresponding DNA sequences and annotations in Galaxy
- Retrieve the metadata associated with these genomes in a table
- Evaluate the genome diversity of the dataset using rapid pairwise comparisons, and dereplicate the dataset of necessary
time_estimation: 1H
key_points:
- The **ncbi-dataset** tool simplifies the download of genome data and metadata from the Genbank and RefSeq repositories
- The **dRep** tool analyses genome diversity within a bacterial genome dataset.
- Depending on the features of the dataset and the scientific question, it is advisable to **dereplicate the genome dataset** using adjusted clustering parameters. This involves selecting the highest quality representative genomes and removing those that are nearly identical and do not provide valuable additional genomic content.
contributions:
  authorship:
  - hchiapello
  - bebatut
  - vloux
editing:
  - bebatut
testing:
  - hchiapello
  - vloux
  - bebatut
funding:
  - elixir-fr
  - INRAE

edam_ontology:
- topic_0622 # Genomics
- topic_3301 # Microbiology
level: intermediate
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

{: .question}

# Get basic information about genome assemblies of your favorite bacterial species / genus from the NCBI repository 

Before building a genome dataset we strongly recommend exploring the genome assemblies of your favourite bacterial species/genus that arer available in public databanks (NCBI, ENA). You will generally be interested in comparing your own private genomes to the public ones.

> <hands-on-title> Get informations on public genomes for your favorite bacteria from NCBI datasets website</hands-on-title>
>
> > 1. Retrieve genome information at NCBI using the website [NCBI Datasets](https://www.ncbi.nlm.nih.gov/datasets/)
>    - Go the NCBI datasets web site
>    - Enter the name of you favorite bacteria in the dark blue frame: here we propose *Streptococcus salivarius* 
>    - Look at the resulting web page.
>
>    > <comment-title> The NCBI TaxId </comment-title>
> 
>     > The **Taxonomy resource** of the National Center for Biotechnology Information (NCBI)  is a curated database of organism names and classifications. It provides links to related data for all taxonomic nodes. It contains organism names and classifications for all sequences in the nucleotide and protein sequence databases of the International Nucleotide Sequence Database Collaboration (INSDC). Each Taxonomy entry or TaxNode includes: a primary name, a number of secondary names and a public stable, unique identifier, the **taxonomy identifier, or TaxId**. Due to the numerous issues with taxonomic nomenclature in bacterial organisms, **we recommend using the TaxId rather than the taxonomic name when building bacterial genomic datasets.** 
>    {: .comment}
>
>
{: .hands_on}

{% snippet topics/genome-annotation/faqs/assembly_levels.md %}

{% snippet topics/genome-annotation/faqs/reference_genomes.md %}
  
> <question-title> Informations on S. salivarius NCBI public genomes</question-title>
>
> 1. What is the **NCBI Taxonomy id** of *S. salivarius*?
> 2. How many **public genomes** are they for *S. salivarius* in NCBI?
> 3. What is the **reference genome** accession number of *S. salivarius* ? 

>
> > <solution-title>Answers about *S. salivarius* public genomes</solution-title>
> > 
> > 1. *S. salivarius* taxonomy id: 1304
> > 2. 518 public *S. salivarius* genomes (date: 2015/08/22)
> > 3. *S. salivarius* reference genome accession is GCF_000253315.1
> >
> {: .solution}
>

> <hands-on-title> Data Retrieval </hands-on-title>
>
> 1. Create a new history for this analysis
>
>    {% snippet faqs/galaxy/histories_create_new.md %}
>
> 2. Rename the history
>
>    {% snippet faqs/galaxy/histories_rename.md %}
>
>
{: .hands_on}

# Create a metadata report for a dataset of genome assemblies 

The **NCBI dataset tool** provides tools to retrieve genome assemblies and related metadata separately. Metadata contains key information about sequencing and assembly quality metrics, such as assembly length and coverage, number of contigs, N50 and L50 metrics ; Biosample features, such as organism, strain, isolation source and geographic location; and annotation results, suche as the number of coding and non-coding genes.
First looking at the metadata allows you to refine the dataset according to different criteria. Then, you can download the genomes on the refined dataset. 
In this tutorial we propose to use the **taxon id** to download important metadata related to public RefSeq genome assemblies of the S. salivarius species.
In comparative bacterial genomics, high-quality genomes with verified assemblies and consistent annotations are often needed. Therefore recommend here using *RefSeq rather than Genbank* as the genome resource.

{% snippet topics/genome-annotation/faqs/refseq_vs_genbank.md %}


{: .hands_on}

> <hands-on-title> Retrieve metadata of the public RefSeq assemblies of your favorite bacteria</hands-on-title>
>
> 
> 1.  Use the Tool {% tool [NCBI Datasets Genomes](toolshed.g2.bx.psu.edu/repos/iuc/ncbi_datasets/datasets_download_genome/16.42.0+galaxy0) %} to generate a report of public genomes of your bacteria 
>   - In *"Query"* - *"Choose how to find genomes to download"*: `By Taxon (NCBI Taxonomy id, scientific or common name)` and enter the taxon id for *S. salivarius* (see above)
>     - In *"Filters and Limit"*: 
>        - set **Assembly source** to `RefSeq` 
>     - In *"Ouput Options"* 
>        - In *"Columns in the report"* add *at least* the following important columns: `Asssembly level, Assembly release data, Assembly sequencing tech, Assembly Stats total number of chromosomes, Assembly stats Total Sequence Length, Assembly Stats Contig N50, Assembly Biosample accession number,Assembly Biosample Collection Date, Assembly Biosample geographic location, Assembly Biosample isolation source`
>         - In *"Include"* For this first query `remove the genomic sequence (genome)` to be able to refine your dataset before downloading the corresponding genomes
> Look at the Result file *NCBI Genome Datasets: Data Report*

> <question-title>Information on *S. salivarius* NCBI RefSeq genomes</question-title>
>
> 1. How many RefSeq public genomes are there in the resulting table S. salivarius ?
> 2. What is the total sequence length of the reference genome of S. salivarius ?
> 3. What can you say about metadata related to the Biosample (i.e. collection date, geographic location, isolation source,...)?
> > <solution-title>*S. salivarius* NCBI RefSeq</solution-title>
> >
> > 1. Number of Refseq S. salivarius genomes: 282 (date: 2015/08/22)
> > 2. The reference genome of S. salivarius has accession number GCF_000253315.1 and has 2.210.574 pb length
> > 3. Regarding Biosample metadata, we observed many missing or unknown/undetermined values. We can also see that many metadata values are not in standard format, for instance for collection dates you may have: year, year-month, or year-month-day values. 
> >
> {: .solution}


# Download a dataset of genome assemblies from NCBI

> <hands-on-title> Use genome IDs to download genomes </hands-on-title>
>
> 1. Extract genome IDs from NCBI genome Data report
> {% tool [Cut](Cut1) %} with the following parameters:
>    - *"Cut columns"*: `c1`
>    - {% icon param-file %} *"From"*: `NCBI Genome Datasets: Data Report` (Input dataset)
>
>  2. {% tool [Remove beginning](Remove beginning1) %} with the following parameters:
>    - *"Remove first"*: `1`
>    - {% icon param-file %} *"from"*: `outfile` (output of **Cut** {% icon tool %})
>
> 3. {% tool [NCBI Datasets Genomes](toolshed.g2.bx.psu.edu/repos/iuc/ncbi_datasets/datasets_download_genome/16.42.0+galaxy0) %} with the following parameters:
>    - In *"Query"*:
>        - *"Choose how to find genomes to download"*: `By NCBI assembly or BioProject accession`
>            - *"Enter accession or read from file ?"*: `Read a list of NCBI Assembly accessions from a dataset`
>                - {% icon param-file %} *"Select dataset with list of NCBI Assembly accessions"*: `out_file1` (output of **Remove beginning** {% icon tool %})
>    - In *"Output options"*:
>       - In *"Include"*: Retrieve all file formats of interest and add Genbank flat files (gbff) and GFF3 files
>
>    > <comment-title> Genome dataset </comment-title>
>    > 
>    > Some results from NCBI Datasets Genome Download are stored in Lists of Lists (List of Lists of datasets).We must "flatten the collection" , ie, do only list of datasets, not list of list. List or dataset Collection (see Galaxy documentation) allow you to group together related datasets into collections that can be processed alltogether. -> Do this for : genome fasta output.
>    {: .comment}
>
{: .hands_on}


# Analyze genome diversity  and optionnaly dereplicate you dataset

The **dRep** tool provides facilities to rapidly compare and dereplicate large dataset of microbial genomes. It can compare a list of genomes in a pairwise manner and identify group of genomes that are very similar in terms of average Nucleotide Identity (ANI).

{% snippet topics/genome-annotation/faqs/ani_genome.md %}

dRep performs this in two steps: first with a rapid primary algorithm (Mash), and second with a more sensitive algorithm (ANIm)

We will first use **dRep compare** to analyze the genome diversity of the *S. salivarius* dataset.


> <hands-on-title> Compare the genomes of the *S. salivarius* dataset </hands-on-title>
>
> 1. Use {% tool [dRep compare](dRep compare) %} with the following parameters:
>    - *"Genomes"*: select `Dataset collection`and the flattened collection of RefSeq complete genomes (list of fasta.gz datasets)
>    - *"Genome comparison and clustering"*: `Default parameters`
>    - *"Select outputs"*: add `Secondary_clustering_dendograms.pdf` file 
> 
> Interpret the Results
>
> 2. Use {% tool [dRep dereplicate](dRep dereplicate) %} with the following parameters:
>   - *"Genomes"*: select `Dataset collection`and the flattened collection of RefSeq complete genomes (list of fasta.gz datasets)
>    - *"Genome comparison and clustering"*:  set the `ANI threshold to form primary clusters`to `0.97`(instead of 0.9) and the `ANI threshold to form secondary clusters`to `0.99` (default value)
>
>
{: .hands_on}


## How to choose the ANI thresholds parameters
Selecting the correct ANI threshold parameters is not straightforward. The default ANI primary clustering threshold is 0.9, which is a quite low-value, while the secondary clustering default threshold is 0.95 (roughly corresponding to ANI species delineation). 
If you know nothing about genome diversity of your dataset, use these default values to run a first **dRep compare** analysis, but be aware that the computation time may be long. You can then use the results of the dRep compare analysis to launch a **dRep dereplicate** using parameters adjusted to your dataset.
In this tutorial, we are dealing with genomes of the same species, meaning that all pairs of genomes should have an ANI value greater than 0.95. This is why we increase the first and second ANI thresholds to 0.97 and 0.99 respectively.


# Last step: construct a dereplicate collection of genomes
>
> <hands-on-title> Prepare the collection of dereplicated *S. salivarius* genomes for further comparative analyses </hands-on-title>
>
> 1. Extract the list of dereplicated genomes id from the dRpep text outfile `Widb.csv` using the {% tool [Cut](Cut1) %} with the following parameters:
>    - *"Cut columns"*: `c1`
>    - *"Delimited by"*: `comma`
>    - {% icon param-file %} *"From"*: `drep dereplicate : Widb.csv` (Input file)
>
> 2. Clean the list of dereplicated genome ids by replacing the genome IDs written by dRep (accession and assembly names) by only accession IDs 
> ex: Replace GCF_009717395.1_GCF_009717395.1_ASM971739v1.fasta by  GCF_009717395.1
> 
> We will use a Regular Expression to do a super powerfull search and replace for each line of the list
> {% tool [Regex Replace](Regex Replace) %} with the following parameters:
>    - *"From"*: `cut on data XXX`
>    - *"Search String"*: `(.\d+)_(GC.*))`
>    - *"Replace String"*: `\1`
>
>  3. Clean the list of dereplicated accessions by removing the first line using {% tool [Remove beginning](Remove beginning1) %}  tool with the following parameters:
>    - *"Remove first"*: `1`
>    - {% icon param-file %} *"from"*: `regex replace on data XXX` 
> 
>  4. Filter the initial S. salivarius genome collection by using the tool {% tool [Filter collection](Filter collection) %} with the following parameters:
>   - {% icon param-file %} *"Input collection"*: `Genbank datasets (flattened)`
>    - *"How should the elements to remove be determined"*: `Remove if identifiers are ABSENT from file`
>    - *"Filter out identifiers absent from"*: `Remove of begining of data xx`.
>  
> This tool will produce two collections: (i) filtered that contains dereplicated genomes and (ii) discarded that contains the remaining genomes. rename the filtered collection and delete the discarded.
> 
{: .hands_on}


# Conclusion

Sum up the tutorial and the key takeaways here. We encourage adding an overview image of the
pipeline used.