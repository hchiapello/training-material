---
title: Assembly types in NCBI genome assemblies
area: genome-annotation
box_type: tip
layout: faq
contributors: [hchiapello]
redirect_from: [/topics/genome-annotation/tutorials/bacterial-comparative-genomics-dataset-construction/assembly_levels]
---

The assembly level of a genome is defined as follows in NCBI Genome dataset documentation:

## Complete genome
All chromosomes are gapless and contain runs of nine or less ambiguous bases (Ns), there are no unplaced or unlocalized scaffolds, and all the expected chromosomes are present (i.e., the assembly is not noted as having partial genome representation). Plasmids and organelles may or may not be included in the assembly, but if they are present, the sequences are gapless. The chromosome sequences may not be fully complete from telomere-to-telomere (T2T).

## Chromosome
There is sequence for one or more chromosomes. This may be a completely sequenced chromosome without gaps or a chromosome containing spans with gaps between them. There may also be unplaced or unlocalized sequences.

## Scaffold
One or more contigs are connected across gaps of 10 or more bases to create scaffolds. All sequences are unplaced or unlocalized.

## Contig
All sequences do not contain gaps. All sequences are unplaced or unlocalized. Includes ultra-contig assemblies based on long read sequencing with no gaps.

