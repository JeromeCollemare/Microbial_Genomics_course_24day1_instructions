*Microbial genomics, Functional annotation, Day 2*

Assignments
===

**Exercise 1: orthologous protein families**

Different fungi exhibit different host specificity or growth, which can be related to their
gene complement. **Genes that are shared across all fungi are expected
to be involved in common biological processes, while genes specific to
certain fungi are more likely to explain their specificity.** Tools exist
to compare gene sequences between species and classify them according to
their similarity to form protein families. One such tool is OrthoFinder
(https://github.com/davidemms/OrthoFinder/releases),
for which you can find the results on the server
(**~/data/fungalgenomics\_collemare/day2/Runld\_31\_counts.txt**).
Open the file in Excel (or similar spreadsheet software) or using the Terminal. OrthoFinder groups proteins in clusters. A cluster shared in different species contain orthologous proteins. Within a given species, a cluster can comprise several proteins, which are then called paralogues (and belong to a
so-called protein family).

> Q1: What does the total number of genes/proteins represent for the
> *Mycosphaerellaceae*?
>
> Q2: Determine the proteome size of each species. How do you explain the differences?

To facilitate further analyses when using a spreadsheet software, create a new column which contains for each cluster (row) the number of species which have proteins belonging to this cluster. When using the Terminal, a command line with awk for example allows filtering the data without creating such a new column.

> Q3: Determine what is the **core** proteome for these fungi? Determine the size of the core proteome \(number of clusters\). Does it have a similar size in each species \(number of proteins\)? Which fraction of the total proteome of each species does the core proteome represent?
>
> Q4: Compare the size of the **specific** proteomes. Does it have a
> similar size in each species? Which fraction of the total proteome of
> each species does it represent? How do you explain these differences?

As we are interested in protein functions, we can now compare which functions are found in the core and specific proteomes. For each cluster, the predicted PFAM conserved domains are indicated. For the following questions, using the Terminal and awk is easier, though it is also possible to do it in the spreadsheet.

> Q5: How many proteins are not assigned any function (*i.e.* no PFAM) in the core and specific proteomes? How many proteins are assigned a function (*i.e.* with a PFAM domain)? What is your conclusion?
>
> Q6: What are the most abundantly represented functions in the core and specific proteomes (focus on the 10 most abundant)?

** **

**Exercise 2: compare the gene content between different species**

In this exercise, you will use a **targeted approach because certain
classes of proteins are known to play crucial roles in the adaptation of
fungi to different ecological niches: secreted-small proteins, secreted
proteases, CAZymes, secondary metabolites**. This targeted approach is
commonly used as a basis for the analysis of any fungal genome. It is
usually good to include contrasting reference genomes as controls; thus,
functional annotations are provided for the baker’s yeast *Saccharomyces
cerevisiae* (Sacce1) and the saprobe *Aspergillus nidulans* (Aspnid1).

Using the annotation files, compare the predicted proteome size of each
plant pathogens to the one of *A. nidulans* and *S. cerevisiae*. Use the
different annotation files to extract the following categories and
sub-categories, and follow the questions to guide your analysis:

Secretome

*Secreted-Small Proteins (SSPs) | Secreted CAZymes | Secreted peptidases/proteases*

Secondary metabolite genes

*Polyketide Synthases (PKSs) | Non-Ribosomal Peptide Synthetases (NRPSs)*

> Q1: Start with general statistics. Write a bash command that makes use
of **wc** to count the total number of proteins in each annotation file. Then, write a bash
command that makes use of **awk** and **wc** to count the number of
proteins with transmembrane domains and the number of proteins that are
predicted to be secreted.
> 
> Q2: How many SSPs are encoded in each genome? Adapt the bash command
with **awk** and **wc** to automatically count the number of SSPs.
>
> Q3: For counting secreted peptidases/proteases, adapt the bash command
using **grep** to retrieve the genes with the terms “peptidase” or
“protease” description in the functional annotation.
>
> Q4: Adapt the previous bash command to retrieve secreted CAZymes
(use the terms “Glyco\_hydro”, “Glyco\_transf” and “CBM” pfam domains in the
functional annotation).
>
>Q5: Adapt the following bash command to retrieve PKS and NRPS proteins,
which are very large proteins, using the signature conserved domains PF02801 (PKS)
and PF00668 (NRPS):
~~~
$ grep "x\|y" funannot.*.txt | awk '{if($z>1000) print $0}' | wc -l
~~~
> Q6: Compare the numbers between all different species. Do you find significant differences between certain species? Does it correlate with their lifestyle? Can you suggest complementary approaches that would allow making more precise assumptions?

** **

**Exercise 3: case study with expression data**

While comparative functional genomics is useful to identify candidate genes, it is usually not sufficient to make robust hypotheses and restrict the selection to a number of genes that is manageable for experimental validation. Additional analyses are therefore needed, which can be of very diverse kind. In this exercise, you will see how gene expression and functional annotation can lead to the identification of genes and functions that could be involved in plant pathogenicity.

**Genes involved in virulence are expected to be specifically
expressed during the infection process**, and not *in vitro*. Here, you will identify categories of genes in *Z. tritici* that are
expressed during infection of wheat as they may be involved in
pathogenicity. The RNAseq data you previously used is available on the
server (**~/data/fungalgenomics\_collemare/day2/Expression.txt**).

a) In Excel (or similar spreadsheet software) or using the Terminal, combine the file that contain FPKM values from *in vitro* and *in planta* conditions (**~/data/fungalgenomics\_collemare/day2/Expression.txt**) with the functional annotation file of *Z. tritici* (**~/data/fungalgenomics\_collemare/day2/_funannot.Mycgr3.txt**).

NB: pay attention to the order of the genes in each file. delete lines that do not start with a gene id.

b) Sort the genes to identify those that are significantly differentially regulated *in planta* and compare the gene content in each category (significantly up- or down-regulated, non-significantly differentially expressed). Follow the questions for your analysis.

NB: to facilitate analyses, it is recommended to create new tabs with selected sets of genes.

> Q1: What is the total number of genes predicted in the genome? Which
column should you use to sort the data and differentiate between
significantly and non-significantly regulated genes? How many genes are
significantly up-regulated *in planta*? How many genes are significantly
down-regulated *in planta*?
>
> Q2: Let’s focus on genes that are commonly associated with virulence,
secreted proteins. Which criteria do you need to use to identify
putatively secreted proteins? What is the size of the predicted
secretome? Compare the number of predicted secreted proteins in each
category (significantly up- and down-regulated).
>
> Q3: What are the characteristics of SSPs? How many of the predicted
up-regulated or down-regulated genes encode SSPs?
>
> Q4: Which functions are represented in the up- or down-regulated SSPs?
>
> Q5: Based on these first results, can you formulate any hypothesis on
potential virulence factors? Can you identify limitations that makes
conclusions difficult to make?
>
> Q6: Another way to analyse this data is to look at the differentially
regulated genes with the most significant difference between the two
conditions, and considering the genes that exhibit the highest
expression on wheat while very low or not expressed *in vitro*. Sort the
data according to these criteria and focus on the first 50 most
significantly expressed genes. How many SSPs are in this list? Can you
identify interesting functions that might be important in the
pathogenicity of *Z. tritici*?


**Exercise 4: case study with secondary metabolism gene clusters**

In this exercise, we will combine a comparative analysis and a phylogenetic analysis to reduce the number of candidate genes. In this case, we will focus on **fungal secondary metabolites which are known to play important roles in
interactions with plants, serving as toxins, defense suppressors or
avirulent signals.** Fungi are famous producers of polyketides and
non-ribosomal peptides. In the previous exercise 2, you already retrieved
the number of these enzymes encoded in the different genomes, but it was
not possible to determine if some of these genes would be important for
pathogenicity on a given host. More precise analyses need to be done.
Secondary metabolite biosynthesis actually involves many more genes than
PKS and NRPS, which for a given pathway co-localize in the genome and
are co-regulated, defining a gene cluster organization. There are
several tools to predict these gene clusters and today you will use the
results of one of them: fungiSMASH (<https://fungismash.secondarymetabolites.org/#!/start>). All genomes
have been analysed with fungiSMASH and the output results are available
online:

Clafu1 <https://fungismash.secondarymetabolites.org/upload/fungi-95eb7527-b8cb-4ccf-b56b-3ee9591f9142/index.html>

Dotse1 <https://fungismash.secondarymetabolites.org/upload/fungi-ad7a37e1-3584-46d0-9bdb-c1b35bb378bc/index.html>

Mycfi2 <https://fungismash.secondarymetabolites.org/upload/fungi-6e56b5a0-2f35-4316-a456-99ccd392f80e/index.html>

Mycgr3 <https://fungismash.secondarymetabolites.org/upload/fungi-6eaadb2b-81e1-4889-bdbe-03bf775d201e/index.html>

Sepmu1 <https://fungismash.secondarymetabolites.org/upload/fungi-cace12de-b62a-498e-8e67-b1753e2bfd38/index.html>

Seppo1 <https://fungismash.secondarymetabolites.org/upload/fungi-87ea7424-0884-44ab-bfc8-1a630714c4c2/index.html>

Aspnid1 <https://fungismash.secondarymetabolites.org/upload/fungi-d6cdaa17-da7f-4e2a-9bd9-9eee430cf631/index.html>

Sacce1 <https://fungismash.secondarymetabolites.org/upload/fungi-94a0176b-d02b-4652-a4fc-59a000bb095b/index.html>

> Q1: Open one of the fungiSMASH result link and check the information given by fungiSMASH on this main page. Click on one region to access more specific information. List the information that is presented on this main summary page and for one region specific page.
>
> Q2: For each species, compare the PKS and NRPS results of antiSMASH to
the functional genome annotation you previously analysed. Are they
similar or different? Which count do you think is more reliable?

PKSs are a large family of highly conserved proteins. It is
straightforward to compare their sequences using phylogenetic analyses
and link them to certain phenotypes. In this exercise, you will
**perform a deeper phylogenetic analysis of fungal PKSs**. For this
purpose, the sequences of the KS and AT conserved domains of PKSs from
each Mycosphaerellaceae species were retrieved and stored in a fasta
file located on the server
(**~/data/fungalgenomics\_collemare/day2/PKS.fasta.txt**).

> Q3: Align the sequences using the multiple sequence alignment tool
mafft (https://mafft.cbrc.jp/alignment/software/), save it in **fasta** format and visualize the alignment using the online tool Mview (https://www.ebi.ac.uk/jdispatcher/msa/mview?stype=protein)
(you can also use other tools like AliView for example). Can you describe the alignment you see?
>
> Q4: Remove poorly aligned regions using trimAl (see manual: https://vicfero.github.io/trimal/),
keeping only positions that are present in at least 60% of all sequences. Visualize the alignment again. Do you notice changes?
>
> Q5: Using the trimmed alignment, build a phylogenetic tree using the FastTree command line (https://manpages.ubuntu.com/manpages/focal/man1/fasttree.1.html); use the LG amino acid substitution model.

Visualize the phylogenetic tree with the online tool iTOL
(https://itol.embl.de) (you need to create a free iTOL account to upload or drag the tree file). Drag and drop the tree file, then in the advanced options on the right (bottom), root the tree with the midpoint method. Format the layout of the tree at your convenience using the different options offered in iTOL. It is recommended to show the bootstrap values using the Advanced tab and only display those above 0.99. To color labels according to the species which thus indicate the host plant, drag and drop the **~/data/fungalgenomics_collemare/day2/day2_itol_annotation.txt** file in iTOL.
NB: you will not be able to save the annotated tree in the free access version.

> Q6: Can you identify a PKS that is common to all species, *ie* a clade with strong bootsrap support
that comprises orthologues only? Can you find which compound this PKS
could produce in all species thanks to results and annotations from fungiSMASH?
>
> Q7: Focusing on Seppo and Sepmu that are both pathogenic on poplar, can you find clades with strong bootstrap support
> that only comprise PKSs for both species? What are the predicted gene clusters?
>
> Q8: Can you identify PKSs that seem to be unique to one species
> and could be candidates for pathogenicity on specific hosts? 
How would you check if these PKSs are present in more distant
species?
