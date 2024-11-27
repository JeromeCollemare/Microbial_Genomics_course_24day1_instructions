*Microbial genomics, Functional annotation, Day 2*

Introduction
===

The functional annotation of predicted proteomes allows researchers to perform comparative functional genomics and identify particular features of the organisms of interest. By comparing different organisms, hypotheses about specific biological processes can be formulated and candidate genes can be prioritized for further experimental validation. A reliable functional annotation based on accurate prediction tools is thus critical in order to make robust hypotheses.

Because a functional annotation remains a prediction, it is always important to integrate this annotation with other information like transcriptomics, proteomics, networks, genomic context, etc.

** **

Yesterday, you executed a few tools that are commonly used to
functionally annotate predicted proteomes. Today, **you will use the
functional annotation** of complete proteomes (pre-computed for you)
**to perform typical comparative genomics analyses**.

A major issue in natural and agricultural ecosystems is diseases caused by fungi which result in dramatic yield losses in crop fields and forest decay. In order to manage these diseases, understanding how fungal pathogens infect their host plant is crucial. An important research field in plant pathology is thus to identify genes that are involved in the pathogenicity process. Understanding fungal
pathogenicity on plants has greatly
benefited from genomics and transcriptomics. Comparative functional genomics is one approach that is commonly used to find candidate genes to further study for a role in virulence.

Plant pathogenic fungi have been extensively studied and common processes and molecular determinants of pathogenicity are understood. These pathogens must sense and grow on their host, differentiate specialized cells for penetration or nutrient uptake, manipulate the host defenses and metabolism, degrade plant tissues and acquire nutrients. Studies in the last 20 years have well established that fungi use secreted-small proteins (SSPs), secreted proteases, secreted carbohydrate-active enzymes (CAZymes) and secondary metabolites (SMs) to invade their hosts. SSPs and SMs are collectively referred to effectors. SSPs are recognized as short (< 300 amino acids) and cysteine-rich (>= 4) peptides harbouring a signal peptide, but no transmembrane domain nor GPI-anchor signal. SMs are produced by complex biosynthetic pathways that are encoded by genes co-localizing in the genome and co-regulated, defining a biosynthetic gene cluster (BGC) organization. These BGCs consists in genes that encode conserved core enzymes and diverse tailoring enzymes.

The selected species from the *Mycosphaerellaceae* are all major plant
pathogens, but they infect different hosts (*Zymoseptoria tritici*
(Mycgr3) is pathogenic on wheat, *Cladosporium fulvum* (Clafu1) is
pathogenic on tomato, *Dothistroma septosporum* (Dotse1) is pathogenic
on pine, *Pseudocercospora fijiensis* (Mycfi2) is pathogenic on banana,
and *Mycosphaerella populorum* (Sepmu1) and *Mycosphaerella populicola*
(Seppo1) are pathogenic on poplar), different organs (*M. populorum*
infects outer wood and bark while *M. populicola* infects leaves), and
exhibit different lifestyles (*C. fulvum* is biotrophic while the other
species are considered hemi-biotrophic).

In different assignments, you will use simplified annotation files that contain the most useful
functional information: gene id, protein length, number of transmembrane
domains (TMHMM prediction), presence of a signal peptide (signalP
prediction) and conserved domains (as determined using INTERPRO SCAN).
These functional annotations are summarized in files located on the
server
(**~/data/fungalgenomics\_collemare/day2/funannot\_\*.txt**;
NB: ignore the lines that do not start with a gene id).
