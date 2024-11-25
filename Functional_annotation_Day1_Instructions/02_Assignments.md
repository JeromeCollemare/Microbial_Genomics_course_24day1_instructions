*Microbial genomics, Functional annotation, Day 1*

Assignments
===

**Exercise 1: annotation using similarity search**

In this exercise, you will determine **if the predicted proteins in *Z. tritici* share sequence similarity with other proteins from other organisms using BLAST**. Two major non-redundant (nr) databases are commonly used: the Swiss-Prot database (572,214 manually annotated and reviewed sequences (10/2024); http://www.uniprot.org) and the NCBI nr database (840,420,260 sequences (11/2024); all non-redundant GenBank CDS translations+PDB+SwissProt+PIR+PRF excluding environmental samples from WGS projects). Because of the size of the NCBI database, you will “blast” the *Z. tritici* proteins against the Swiss-Prot sequences only, which is available on the server (**~/data/fungalgenomics\_collemare/day1/uniprot\_sprot.fasta**).

Before performing a BLAST search locally, a BLAST database must be built. This step had already been done using the following command:
~~~
$ makeblastdb -dbtype prot -in /path/to/uniprot_sprot.fasta
~~~
You can find more information about makeblastdb on the online BLAST manual https://www.ncbi.nlm.nih.gov/books/NBK279690/


a) Using the BLAST manual and its Appendices (https://www.ncbi.nlm.nih.gov/books/NBK279690) or the BLAST help, prepare a suitable BLAST command to search the Swiss-Prot database with *Z. tritici* proteins as query. Follow the questions to guide you towards the needed command line.
 
> Q1: Which BLAST tool do you need to compare protein queries to protein databases?
>
> Q2: Which arguments do you have to use in any basic BLAST command?
>
> Q3a: Execute a test BLAST search using the file on the server
> .**~/data/fungalgenomics\_collemare/day1/Mycgr3.100000.fasta**,
> which contains a single sequence, and save the results in a text file.
>
> Q3b: Open the result file. List the different information that are
> reported. Which information do you think is important to report for each
> gene when making a large tabular annotation file? Is the output format
> convenient to build an annotation file?
>
> Q3c: Let’s start with the output format. Which argument can you use to
> output the results in a tabular format? Test your command line with a
> single sequence first and save the results in a file.
>
> Q3d: Open the result file: which information is indicated in each
> column? Why does the result file contain more than one line? Are all
> results strongly supported?
>
> Q4: A fungal genome typically contains 10-12k genes. It is therefore
> not very handy to report several subject sequences for each protein
> and it is usually preferred to report the best hit only. Which
> argument can you use in the command line to report only the best hit
> per query sequence? Test your command line with a single sequence
> first and save the results in a file. Open the file and check if the result corresponds to your expectation.

b) Now that you are familiar with blast command lines, run a blast
search for the first 30 annotated proteins of *Z. tritici* using the file on the server
.**~/data/fungalgenomics\_collemare/day1/Mycgr3.30proteins.fasta**
(the run should last around 5 minutes).

> Q5a: Open the result file. Do you have only one result per query
> sequence as expected? How many query sequences have more than one hit
> (you can use a simple bash command using cut, uniq and sort to calculate the
> numbers)?
>
> Q5b: The different reported regions for a single query are
> high-scoring pairs (HSPs). Quite often, one HSP is more significant
> than others. For the annotation file, it is thus sensible to report
> only one HSP. Which argument can you use to limit the number of
> reported HSPs? Test your command line and
> save the results in a file. Check if the results meet your expectations.
>
> Q5c: Open the result file. Do all proteins share
> similarity with proteins from the Swiss-Prot database? If not, is
> there another argument that you could use to keep only the most
> relevant hits (choosing an arbitrary threshold)? Test your command line to exclude the non-reliable
> results. What is the biological meaning when a protein does not share
> sequence similarity with any other sequence?

** **

**Exercise 2: search for conserved domains**

In this exercise, you will determine **if proteins from *Z. tritici*
contain conserved domains that might be involved in specific
functions**. There are many databases and tools to search for conserved
domains. One of the most used databases is PFAM (fully integrated in InterPro since January 2023)
(https://pfam-legacy.xfam.org).
It contains families that are represented by multiple sequence
alignments and derived Hidden Markov Models (HMMs). To search this
database, you need to use hmmscan (search an hmm database with sequence
query) from the HMMER tool suite.

The PFAM database consists of HMMs and was prepared using the command
below:
~~~
$ hmmpress /path/to/Pfam-A.hmm
~~~

It is available on the server
(**~/data/fungalgenomics\_collemare/day1/Pfam-A.hmm**).

a) Using the HMMER3 manual (http://eddylab.org/software/hmmer3/3.1b2/Userguide.pdf) or the hmmscan help, prepare a suitable hmmscan command line to search the PFAM database with *Z. tritici* proteins as query. Follow the questions to guide you towards the needed command line.

> Q1a: Execute a test HMMSCAN search with the minimum number of
> arguments and using the file **~/data/fungalgenomics\_collemare/day1/Mycgr3.100proteins.fasta**
> and PFAM database. Save the results in a text file (the run should last about one minute).
>
> Q1b: Open the result file. List the information you find. Given what you learnt with
> BLAST, which features do you think are important to consider when
> searching for similarities with conserved domains?
>
> Q1c: Should you output only the best hit as you did in the BLAST
> analysis?
>
> Q2a: Which argument can you use to output the results in a tabular
> format? Test your command line and save the results in a file.
>
> Q2b: Which argument can you use to not include hits with low support?
> Test your command line and save the result in a file. You can try
> different arguments and compare the different results.

b) dbCAN (<http://bcb.unl.edu/dbCAN2/>) is a more specific database dedicated to carbohydrate-active enzymes. This is an important family of proteins that play crucial roles in the adaptation of fungi to grow on certain carbon sources. Similar to PFAM, dbCAN contains HMMs that can be used to annotate proteins. You will use this second database to compare results with the PFAM database.
 
The dbCAN database was prepared using the same command as for PFAM and is available on the server (**~/data/fungalgenomics\_collemare/day1/dbCAN-fam.hmm**).
 
> Q3: Execute a HMMSCAN search using the file **~/data/fungalgenomics\_collemare/day1/Mycgr3.100proteins.fasta**
> and the dbCAN database, and save the results in a text file.
>
> Q4: Compare the results you obtained with the PFAM and dbCAN
> databases: are the predictions identical? How do you explain
> differences?
>
> *Optional: In order to analyse the results more easily, it is possible
> to modify the HMMSCAN output to see all domains for a given gene on
> the same line. For this, execute the following command on the PFAM and
> dbCAN output:*
~~~
$ grep -v '^#' output.file | awk '{y=$3;$3="";a[y]=a[y]"\t"$1}END{for(y in a)print y,a[y]}' | sort -k 1 > day1_hmm_oneline.txt
~~~

** **

**Exercise 3: search for conserved motifs**

In this exercise, you will determine **if proteins from *Z. tritici*
contain conserved motifs**. These motifs or patterns often indicate specific protein
structures or sub-cellular localization. Again, there are many different
tools, but you will test three that are commonly used: signalP and tmhmm predicts
signal peptides and transmembrane domains respectively, while targetP predict sub-cellular
localizations.

a) Using SignalP
    (https://services.healthtech.dtu.dk/services/SignalP-4.1/),
    tmhmm (https://services.healthtech.dtu.dk/services/TMHMM-2.0/), and
    TargetP
    (https://services.healthtech.dtu.dk/services/TargetP-2.0/)
    manuals or help, prepare suitable commands.
 
> Q1: Execute the three searches with the minimum number of arguments
> (if any) and using the file
> **~/data/fungalgenomics\_collemare/day1/Mycgr3.100proteins.fasta**.
> Save the results in text files.
>
> NB: help of tmhmm is not easy to find, for a short output, use the parameter --short
>
> Q2: Open the result files: which information is the most interesting in each case?

b) Compare the results from the three tools. Are they all consistent? Start by finding the proteins predicted to
contain a signal peptide and compare the predictions with the other tools. Then continue with transmembrane predictions and
compare signalP and tmhmm.

c) You used SignalP 4.0, tmhmm 2.0 and TargetP 2.0. Updates or new tools are regularly released and often lead to more accurate predictions. SignalP 6.0 and deepTMHMM 1.0 are newer versions of the tools you used and they are available online (https://services.healthtech.dtu.dk/services/SignalP-6.0/ and https://services.healthtech.dtu.dk/services/DeepTMHMM-1.0/).

Using the file **~/data/fungalgenomics\_collemare/day1/Mycgr3.100proteins.fasta**, run these tools with the online interface wiht parameters for Eukaryotes and short outputs.

> Q3: For each tool, compare the results between the version you used and the later version. Are they all consistent?
> Can you identify an example where different predictions could have a strong implication on the prediction of the sub-cellulare localization? How do you evaluate the accuracy of the different predictions?

