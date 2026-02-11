---
title: Reference genomes in NCBI genome assemblies
area: genome-annotation
box_type: tip
layout: faq
contributors: [hchiapello]
redirect_from: [/topics/genome-annotation/tutorials/bacterial-comparative-genomics-dataset-construction/reference_genomes]
---

## Reference genome selection in prokaryotes

**Reference genomes** are only selected for species with formal names accepted under the **International Code of Nomenclature of Prokaryotes (governed by the International Committee on Systematics of Prokaryotes)**, species with names that have conventions for formal use, or Candidatus species. The following genome assemblies are considered in the selection of reference genomes:

- Live RefSeq genome assemblies that are not superseded by newer assemblies or suppressed due to quality or taxonomic misassignment concerns.
- Assemblies that pass Average Nucleotide Identity (ANI) criteria and are:
1. from type material, or
2. not from type material but match type material assemblies for the species at above 70% coverage, or
3. not from type material and, in the absence of type material for the species, are not flagged as mismatches at or above ANI thresholds with at least 70% query and subject coverage to a type from a different species.

A reference genome is chosen among eligible assemblies based on the criteria below, in order of importance:

1. **Manual selection:** a few references are selected based on community input, biological features or other a priori knowledge about the assembly.
2. **Magnitude of deviation from the mean assembly length for the species:v assemblies with the lowest integral number of standard deviations from the species average assembly length are preferred. This ensures that assemblies that are significantly longer or shorter than others for the species are not chosen.
3. **CheckM completeness:** assemblies with the highest level of completeness, as determined by CheckM.
4. **Magnitude of count of pseudo CDSs:** assemblies with the lowest rounded natural log of pseudo CDSs are preferred.
5. **Presence of a plasmid:** assemblies containing plasmid sequences are preferred.
6. **Magnitude of count of scaffolds:** assemblies with the lowest rounded log base 10 scaffold count are preferred.
7. **Species reference:** the current reference is preferred.
8. **Magnitude of deviation from the mean gene count for the species:** assemblies with the lowest integral number of standard deviations from the species average count of genes are preferred. This ensures that assemblies that have significantly more or fewer genes than others for the species are not chosen.
9. **Absolute count of pseudo CDSs:** assemblies with fewer pseudo CDSs are preferred.
10. **Type strain status**
11. **Release date**

## Reference genome update frequency in prokaryotes

Reference genomes are updated weekly to create references for new species that do not have a reference genome and to correct any inconsistencies in the set of references from taxonomic merges. Less frequent updates are performed to account for new RefSeq assemblies, taxonomy updates, and recently discovered contamination.

s