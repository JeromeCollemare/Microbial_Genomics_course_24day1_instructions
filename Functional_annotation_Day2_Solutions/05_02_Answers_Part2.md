*Microbial genomics, Functional annotation, Day 2*

Answers Part 2
===

**Exercise 3: case study with expression data**

a) In Excel (or similar spreadsheet software) or using the Terminal, combine the file that contain FPKM values from *in vitro* and *in planta* conditions (**~/data/fungalgenomics\_collemare/day2/Expression.txt**) with the functional annotation file of *Z. tritici* (**~/data/fungalgenomics\_collemare/day2/_funannot.Mycgr3.txt**).

NB: pay attention to the order of the genes in each file. delete lines that do not start with a gene id.

> *Answer: open the _funannot.Mycgr3.txt file and sort the functional annotation according to the gene id. Next to the annotation, import the Expression.txt data (tab-delimited). Normally, all the data should be sorted, so that the annotation and the expression data of each gene is on the same row. See results_exercise3.xlsx first tab.*

b) Sort the genes to identify those that are significantly differentially regulated *in planta* and compare the gene content in each category (significantly up- or down-regulated, non-significantly differentially expressed). Follow the questions for your analysis.

Q1: What is the total number of genes predicted in the genome? Which
column should you use to sort the data and differentiate between
significantly and non-significantly regulated genes? How many genes are
significantly up-regulated *in planta*? How many genes are significantly
down-regulated *in planta*?

> *Answer: sort the data according to the significance of the q value. Z. tritici genome contains 10,933 predicted genes. Out of those, 1,548 and 1,611 are significantly up-regulated and down-regulated, respectively. Thus, the vast majority of the genes, 7,774, are not significantly differentially regulated. About the same number of genes are up or down regulated in planta compared to in vitro. See results_exercise3.xlsx second tab.*

Q2: Let’s focus on genes that are commonly associated with virulence,
secreted proteins. Which criteria do you need to use to identify
putatively secreted proteins? What is the size of the predicted
secretome? Compare the number of predicted secreted proteins in each
category (significantly up- and down-regulated).

> *Answer: proteins that are most likely secreted should contain a predicted signal peptide and no transmembrane domain (sort according to q value significance, signal peptide and number of TM domains). 728 genes encode putative secreted proteins. Out of those, 123 and 99 are significantly up- and down-regulated, respectively. See results_exercise3.xlsx second tab.*

Q3: What are characteristics of SSPs? How many of the predicted up-regulated or down-regulated genes encode SSPs?

> *Answer: SSPs are secreted proteins that are shorter than 300 amino acids (by convention) and contains several cysteine residues (this data is not available for you, so it is not considered here). Add an additional sorting according to the protein length. There is a total of 327 SSPs encoded in the genome, out of which 56 and 52 are significantly up- and down-regulated, respectively.*

Q4: Which functions are represented in the up- or down-regulated SSPs?

> *Answer: 35 out of 56 up-regulated SSPs do not have any conserved domain, which is a very common feature of SSPs. It is difficult to know what could be their role. Other interesting functions are 2 hydrophobins (Mycgr3|95491 and Mycgr3|96543), 2 proteases (Mycgr3|30802 and Mycgr3|91252), two putative toxic effectors (Mycgr3|111636 and Mycgr3|88451), one chloroperoxidase (Mycgr3|67060) and 3 carbohydrate-active enzymes (Mycgr3|105871, Mycgr3|74453 and Mycgr3|30121), which are functions that have been reported in the virulence of other plant pathogens.*
>
> *33 out of 52 down-regulated SSPs do not have any conserved domain. 1 hydrophobin (Mycgr3|48129), 3 carbohydrate-active enzymes (Mycgr3|33493, Mycgr3|104658, Mycgr3|71724) and 2 proteases (Mycgr3|76021, Mycgr3|49854) are also down-regulated and thus are unlikely involved in virulence. Surprisingly, proteins known to play a role in virulence are also down-regulated here: cerato-platanin toxin (Mycgr3|39947), CFEM-domain effectors (Mycgr3|94274, Mycgr3|98580) and LysM effector (Mycgr3|111221).*

Q5: Based on these first results, can you formulate any hypothesis on
potential virulence factors? Can you identify limitations that makes
conclusions difficult to make?

> *Answer: the significantly up-regulated SSPs are good candidates to further study. When analysing such results, it is important to keep in mind that you are using only one time point during infection of wheat. But pathogenicity is a dynamic process and different set of genes are up-regulated at different time points during infection.*

Q6: Another way to analyse this data is to look at the differentially
regulated genes with the most significant difference between the two
conditions, and considering the genes that exhibit the highest
expression on wheat while very low or not expressed *in vitro*. Sort the
data according to these criteria and focus on the first 50 most
significantly expressed genes. How many SSPs are in this list? Can you
identify interesting functions that might be important in the
pathogenicity of *Z. tritici*?

> *Answer: 3 SSPs are particularly highly expressed in planta (Mycgr3|77055, Mycgr3|102996, Mycgr3|111505; Mycgr3|78594 is actually not an SSP because it is predicted to be anchored in the membrane). Three secreted chloroperoxidase enzymes are highly expressed (Mycgr3|74298, Mycgr3|43487, Mycgr3|63538). Several putative transcription factors are highly up-regulated (Mycgr3|104366, Mycgr3|40797, Mycgr3|67865) and could be involved in regulating sets of pathogenicity genes. See results_exercise3.xlsx third tab.*

** **

**Exercise 4: case study with secondary metabolism gene clusters**

**Fungal secondary metabolites are known to play important roles in
interactions with plants, serving as toxins, defense suppressors or
avirulent signals.** Fungi are famous producers of polyketides and
non-ribosomal peptides. In the previous exercise, you already retrieved
the number of these enzymes encoded in the different genomes, but it was
not possible to determine if some of these genes would be important for
pathogenicity on a given host. More precise analyses need to be done.
Secondary metabolite biosynthesis actually involves many more genes than
PKS and NRPS, which for a given pathway co-localize in the genome and
are co-regulated, defining a gene cluster organization. There are
several tools to predict these gene clusters and today you will use the
results of one of them: fungiSMASH (<https://fungismash.secondarymetabolites.org/#!/start>).

Q1: Open one of the fungiSMASH result link and check the information given by fungiSMASH on this main page. Click on one region to access more specific information. List the information that is presented on this main summary page and for one region specific
page.

> *Answer: the output of fungiSMASH is very visual. On the first page, you find a summary of the results with a short description of regions that contain biosynthetic gene clusters and are found on each contig/scaffold/chromosome. The position is indicated as well as if a known gene cluster is found similar. When you click on one region, you access more detailed results with a description of the locus where the core gene like PKSs and NRPSs are indicated (for which the conserved domains are shown at the bottom). The KnownClusterBlast tab shows if there is a known gene cluster similar to that predicted one. The right side of the window contains additional predictions (not very reliable for fungi), information and links.*

Q2: For each species, compare the PKS and NRPS results of antiSMASH to
the functional genome annotation you previously analysed. Are they
similar or different? Which count do you think is more reliable?

> *Answer: the numbers are quite different, which is explained by the different methods to retrieve the genes. Your previous analysis was rough and could not differentiate particular enzymes like hybrid PKS-NRPs. In contrast, fungiSMASH uses HMMs to find the genes and report the conserved domains. In this regard, it is much more accurate. However, the reported numbers are also different from published manual curation analyses (for example, published Clafu analysis reports 10 PKSs, 10 NRPSs and 2 hybrid PKS-NRPSs). FungiSMASH, as a prediction tool, provides a starting point for further more detailed analyses.*

PKSs are a large family of highly conserved proteins. It is
straightforward to compare their sequences using phylogenetic analyses
and link them to certain phenotypes. In this exercise, you will
**perform a deeper phylogenetic analysis of fungal PKSs**. For this
purpose, the sequences of the KS and AT conserved domains of PKSs from
each Mycosphaerellaceae species were retrieved and stored in a fasta
file located on the server
(**~/data/fungalgenomics\_collemare/day2/PKS.fasta.txt**).

Q3: Align the sequences using the multiple sequence alignment tool
mafft (https://mafft.cbrc.jp/alignment/software/), save it in **fasta** format and visualize the alignment using the online tool Mview (https://www.ebi.ac.uk/jdispatcher/msa/mview?stype=protein)
(you can also use other tools like AliView for example). Can you describe the alignment you see?

> *Answer: You can see in the alignment that certain parts are well conserved, but others are not. Certain regions of the alignment are present in a few species only, adding gaps in the alignment. Robust phylogenetic analyses can only be performed using properly aligned sequences. Alignments can be improved by changing the parameters of the alignment tools, removing poorly aligned sequences or removing poorly aligned regions.*

Q4: Remove poorly aligned regions using trimAl (see manual: https://vicfero.github.io/trimal/),
keeping only positions that are present in at least 60% of all sequences. Visualize the alignment again. Do you notice changes?

> *Answer: Using trimAl has shortened the alignment to 2,094 positions only, which are correctly aligned and are thus informative. The alignment contains much fewer gaps than before.*

Q5: Using the trimmed alignment, build a phylogenetic tree using the FastTree command line (https://manpages.ubuntu.com/manpages/focal/man1/fasttree.1.html); use the LG amino acid substitution model.

Visualize the phylogenetic tree with the online tool iTOL
(https://itol.embl.de) (you need to create a free iTOL account to upload or drag the tree file). Drag and drop the tree file, then in the advanced options on the right (bottom), root the tree with the midpoint method. Format the layout of the tree at your convenience using the different options offered in iTOL. It is recommended to show the bootstrap values using the Advanced tab and only display those above 0.99. Color labels according to the species which thus indicate the host plant.
NB: you will not be able to save the annotated tree in the free access version.

Q6: Can you identify a PKS that is common to all species, ie a clade with strong bootsrap support that comprises orthologues only? Can you find which compound this PKS could produce in all species thanks to results and annotations from fungiSMASH?

> *Answer: a single clade contains orthologues only in all species, which contains Clafu191425, Dotse47338, Mycfij216850, Mycgr96592, Seppo118889 and Sepmu159092. If you search the fungiSMASH results, you will find that these PKSs are related to the melanin pathway. Another method is to take one of the sequences and perform a BLAST search at NCBI, which will indicate as closest relatives DHN melanin synthases. This pigment is important for fungi and the pathway is found conserved in nearly the whole fungal kingdom.*

Q7: Focusing on Seppo and Sepmu that are both pathogenic on poplar, can you find clades with strong bootstrap support that only comprise PKSs for both species? What are the predicted gene clusters?

> *Answer: Here, we wnat to find clades with strong bootstrap support that only contains PKSs from both Seppo and Sepmu.
> Only two clades meet these criteria: Sepmu131426/Seppo20752 and Sepmu154926/Seppo96962. These candidate PKSs could be involved in pathogenicity on their common host.*
> 
> *You can find predicted gene clusters using the fungiSMASH results or the corresponding genome browsers. For example, the locus for Sepmu154926 and Seppo96962 appear conserved in both species and a predicted gene cluster suggest a cytochrome P450 in addition to the PKS.*

Q8: Can you identify PKSs that seem to be unique to one species and could be candidates for pathogenicity on specific hosts? How would you check if these PKSs are present in more distant species?

> *Answer: Several PKSs appear unique to single species: Sepmu151975, Seppo102749, Mycfij20039, Mycfij29867,
> Sepmu166720,Mycgr47832, Dotse90367 and Mycgr90362 appear to be specific. Clafu196875, Clafu188153, Mycgr62978, Dotse180045 and Sepmu164461 are all related to other PKSs, but they appear to originate from duplications in the respective species, suggesting a potential specific function. Actually, Sepmu164461 is highly up-regulated during infection of poplar and might be involved in infecting bark.*
> 
> *A BLAST search with these sequences would allow you determining whether these genes have orthologues in more distant fungal species.*
