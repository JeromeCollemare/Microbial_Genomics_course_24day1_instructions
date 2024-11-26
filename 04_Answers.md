*Microbial genomics, Functional annotation, Day 1*

Answers
===

**Exercise 1: annotation using similarity search**

a) Using the BLAST manual (https://www.ncbi.nlm.nih.gov/books/NBK279690/) or the BLAST help, prepare a suitable BLAST command to search the Swiss-Prot database with *Z. tritici* proteins as query. Follow the questions to guide you towards the needed commend line.

Q1: Which BLAST tool do you need to compare protein queries to protein databases?

> *Answer: BlastP is dedicated to search similarities between protein
> sequences*
 
Q2: Which arguments do you have to use in any BLAST command?

> *Answer:* blastp -db database\_name -query input\_file\
*these two arguments tell BLAST to compare sequences in the -query to sequences in the -db*

Q3a: Execute a test BLAST search using the file on the server **~/data/fungalgenomics_collemare/day1/Mycgr3.100000.fasta**, which contains a single sequence, and save the results in a text file.

~~~
$ blastp -db uniprot_sprot.fasta -query Mycgr3.100000.fasta > blast_result1.txt
~~~
 
Q3b: Open the result file. List the different information that are reported. Which ones do you think are important to report for each gene when making a large tabular annotation file? Is the output format convenient to build an annotation file?

> *Answer: in the result file, you first find information about the
> database and your query sequence. Then, a list with the names of
> sequences in the database (also called subject) that share
> similarities with your query sequence, including a score (bits) and an
> E-value which indicate how significant are the similarities. Below,
> for each reported subject sequence is shown the alignment with the
> query sequence, as well as more specific information about this
> alignment: length of the alignment, score, E-value, number of
> identical positions, number of similar positions, number of gaps. At
> the end of the file, are indicated the parameters used by BLAST to
> perform the search.*
>
> *When assigning a function, it is important to only show reliable
> information. The name and description of the subject sequences, as
> well as the reliability of the result given by E-values or scores are
> important. The bitscore derives directly from the alignment, meaning
> that the more identical two sequences, the higher the score. However,
> it does not consider the size of the database which has a direct
> impact on the false discovery rate. E-values are scores normalized to
> the size of the database and thus provide an estimation of the chance
> to find similarity by random. Thus, the lower the E-value, the more
> significant the hit. Protein identity/similarity is also an important
> information to keep because it indicates how distantly related the
> query and subject proteins are. The length of the alignment can be
> useful because it will indicate the protein coverage of the alignment,
> meaning how much of the query and subject sequences are aligned. A
> significant alignment over a very short portion of the query sequence
> would not provide very strong information about the function of the
> protein.*
>
> *The default output format is not convenient as alignments themselves
> are not necessary. A tabular format is more useful.*

Q3c: Let’s start with the output format. Which argument can you use to output the results in a tabular format? Test your command line with a single sequence first and save the results in a file.

~~~ 
$ blastp -db uniprot_sprot.fasta -query Mycgr3.100000.fasta -outfmt 6 > blast_result2.txt
~~~
 
Q3d: Open the result file: which information is indicated in each column? Why does the result file contain more than one line? Are all results strongly supported?

> *Answer: name of query sequence | name of subject sequence | identity
> percentage | alignment length | number of identical positions | number
> of gaps | start position in query sequence | end position in query
> sequence | start position in subject sequence | end position in
> subject sequence | e-value | bit score*
>
> *The file contains several lines because one query sequence can align
> to different subject sequences in the database.*
>
> *Apart from the first three subject sequences, all other exhibit a
> high e-value and low bit score, corresponding to short alignments with
> low similarity. These results are not reliable and should not be
> consider for predicting protein function.*

Q4: A fungal genome typically contains 10-12k genes. It is therefore not very handy to report several subject sequences for each protein and it is usually preferred to report the best hit only. Which argument can you use in the command line to report only the best hit per query sequence? Test your command line with a single sequence first and save the results in a file. Assess the result.

~~~ 
$ blastp -db uniprot_sprot.fasta -query Mycgr3.100000.fasta -max_target_seqs 1 -outfmt 6 > blast_result3.txt
~~~

> *Answer:*
> *Only the best hit is now reported.*

b) Now that you are familiar with blast command lines, run a blast search for the first 30 annotated proteins of *Z. tritici*.

~~~ 
$ blastp -db uniprot_sprot.fasta -query Mycgr3.30proteins.fasta -max_target_seqs 1 -outfmt 6 > blast_result4.txt
~~~

Q5a: Open the result file. Do you have only one result per query sequence as expected? How many query sequences have more than one hit (use a simple bash command using cut, uniq and sort to calculate the numbers)?
 
> *Answer: For 2 genes, there are 2 to 3 hits (bash command is
> :* cut -f1 blast\_result4.txt | uniq -c | sort -r*). *For a given gene, they correspond to high-scoring segment pair (HSPs), meaning that different regions of the subject protein align with the query protein with a gap in between. It is commonly found when either the query or subject sequence contains a deletion.*

Q5b: The different reported regions for a single query are high-scoring pairs (HSPs). Quite often, one HSP is more significant than others. For the annotation file, it is thus sensible to report only one HSP. Which argument can you use to limit the number of reported HSPs? Test your command line and save the results in a file. Check if the results meet your expectations.

~~~ 
$ blastp -db uniprot_sprot.fasta -query Mycgr3.30proteins.fasta -max_target_seqs 1 -max_hsps 1 -outfmt 6 > blast_result5.txt
~~~
 
Q5c: Open the result file. Do all proteins share similarity with proteins from the Swiss-Prot database? If not, is there another argument that you could use to keep only the most relevant hits (choosing an arbitrary threshold)? Test your command line to exclude the non-reliable results. What is the biological meaning when a protein does not share sequence similarity with any other sequence?

> *Answer: 5 proteins (Mycgr3|100080, Mycgr3|100157, Mycgr3|100264,
> Mycgr3|100300, Mycgr3|100533) show results with clear high e-value,
> meaning that these results are not reliable. It can be concluded that
> these five proteins are not sharing any sequence similarity with any
> known sequence and are specific to Z. tritici. Such proteins may
> indicate a new biological function reflecting adaptation of Z. tritici
> to its specific environment.*
>
> *An argument that could be used to report only significant hits is
> -evalue:*
~~~
$ blastp -db uniprot_sprot.fasta -query Mycgr3.30proteins.fasta -max_target_seqs 1 -max_hsps 1 -evalue 0.001 -outfmt 6 > blast_result6.txt
~~~
> *The significant threshold is an arbitrary choice. You can use more stringent e-values if you
> want to increase the accuracy of the results.*

** **

**Exercise 2: search for conserved domains**

a) Using the HMMER3 manual (http://eddylab.org/software/hmmer3/3.1b2/Userguide.pdf) or the hmmscan help, prepare a suitable hmmscan command line to search the PFAM database with *Z. tritici* proteins as query. Follow the questions to guide you towards the needed command line.

Q1a: Execute a test HMMSCAN search with the minimum number of arguments and using the file **~/data/fungalgenomics_collemare/day1/Mycgr3.100proteins.fasta** and PFAM database. Save the results in a text file (the run should last about one minute).

~~~ 
$ hmmscan -o day1_hmm_result1.txt Pfam-A.hmm Mycgr3.100proteins.fasta
~~~

Q1b: Open the result file. List the information you find. Given what you learnt with BLAST, which features do you think are important to consider when searching for similarities with conserved domains?

> *Answer: for each query sequence, a table present the conserved
> domains that present domain hits, with a summary of significance
> values (E-value, score, and bias applied to the score to consider
> sequence composition) and domain description. Then, for each conserved
> domain is shown the alignment between the domain and query sequence.
> Below are presented statistics summary of the analysis.*
>
> *Description of the conserved domains, reliability of the results
> given by e-values and scores; suitable format of the output: one line
> per protein.*

Q1c: Should you output only the best hit as you did in the BLAST analysis?

> *Answer: in the BLAST search, we limited the results to the best hit
> because we were looking at homologous proteins. A protein can consist
> in several conserved domains and thus it is important to keep all
> significant hits because they might provide different useful information
> about the putative biological activity.*

Q2a: Which argument can you use to output the results in a tabular format? Test your command line and save the results in a file.

~~~ 
$ hmmscan --tblout day1_hmm_result2_tblout.txt -o day1_hmm_result2_main.txt Pfam-A.hmm Mycgr3.100proteins.fasta
~~~

> *Answer:*
> *Note that the --tblout argument prints the tabular results in a file.
> But the main standard output can still be saved in another file using
> the -o argument.*

Q2b: Which argument can you use to not include less-supported hits? Test your command line and save the result in a file. You can try different arguments and compare the different results.

> *Answer: several arguments can be used to keep very significant
> results only (reporting thresholds, inclusion thresholds,
> model-specific thresholds). The model-specific thresholds are
> certainly good to use when using curated databases like PFAM
> (--cut\_ga argument), but the default reporting threshold (-E
> argument) could be used with different databases in order to use the
> same threshold for all.*
>
> *Here, we choose the -E argument for a 0.0001 threshold, which was
> chosen for stringent results.

b) dbCAN (<http://bcb.unl.edu/dbCAN2/>) is a more specific database dedicated to carbohydrate degrading enzymes. This is an important family of proteins that play crucial roles in the adaptation of fungi to grow on certain carbon sources. Similar to PFAM, dbCAN contains HMMs that can be used to annotate proteins. You will use this second database to compare results with the PFAM database.

The dbCAN database was prepared using the same command as for PFAM and is available on the server (**~/data/fungalgenomics\_collemare/day1/dbCAN-fam.hmm**).

Q3: Execute a HMMSCAN search using the file **~/data/fungalgenomics\_collemare/day1/Mycgr3.100proteins.fasta** and the dbCAN database, and save the results in a text file

~~~
$ hmmscan -E 0.0001 --tblout day1_hmm_result4_tblout.txt -o day1_hmm_result4_main.txt dbCAN-fam.hmm Mycgr3.100proteins.fasta
~~~

Q4: Compare the results you obtained with the PFAM and dbCAN databases: are the predictions identical? How do you explain differences?

> *Answer: the search in the dbCAN database gives much fewer results,
> which is logical given that only proteins that are related to
> carbohydrate-active enzymes are reported (8 in the case of this
> dataset). While for most proteins, predictions are consistent, for
> two, the predictions do not seem to agree (Mycgr3|100000,
> Mycgr3|100584). In the case of Mycgr3|100000, it could be that the
> prediction with dbCAN is not fully robust because the e-value is much
> lower than with PFAM. In the case of Mycgr3|100584, it could be
> similar, but the dbCAN search could also provide more precise
> information compared to the results with PFAM. It shows that it is
> good to perform the same analysis using different databases.*

** **

**Exercise 3: search for conserved motifs**

a) Using SignalP
    (https://services.healthtech.dtu.dk/services/SignalP-4.1/),
    tmhmm (https://services.healthtech.dtu.dk/services/TMHMM-2.0/), and
    TargetP
    (https://services.healthtech.dtu.dk/services/TargetP-2.0/)
    manuals or help, prepare suitable commands.
 
Q1: Execute the three searches with the minimum number of arguments
(if any) and using the file
**~/data/fungalgenomics\_collemare/day1/Mycgr3.100proteins.fasta**.
Save the results in text files.

NB: help of tmhmm is not easy to find, for a short output, use the parameter --short

~~~
$ signalp Mycgr3.100proteins.fasta > day1_signalp.txt
$ tmhmm --short Mycgr3.100proteins.fasta > day1_tmhmm.txt
$ targetp -fasta Mycgr3.100proteins.fasta > day1_targetp.txt
~~~

Q2: Open the result files: which information is the most interesting in each case?
> *Answer: SignalP 4.1 predicts signal peptides using neural networks.
> For each sequence, SignalP summarises in column “?” if a signal peptide is
> present (Y) or not (N), according to the given discriminative score
> (D) for neural networks*
>
> *tmhmm 2.0 predicts transmembrane helices using hidden Markov models. In the short output,
> the most informative column is "PredHel", which summarizes the number of predicted transmembrane helices, i.e. transmembrane domains.
> The "Topology" information is useful to know the position of the predicted helices in the protein.*
> 
> *TargetP 2.0 uses machine learning to predict mitochondrial
> target peptide (mTP), signal peptide (SP; and in this case the cleavage site CS), or other location (OTHER).
> The summary of the results is in the column "Prediction"*

b) Compare the results from the three tools. Are they all consistent? Start by finding the proteins predicted to
contain a signal peptide and compare the predictions with the other tools. Then continue with transmembrane predictions and
compare signalP and tmhmm.

> *Answer: signalP predicts a signal peptide in 10 proteins. In addition, signalP predicts
> 12 proteins to contain an N-terminal transmembrane domain. TMHMM predicts transmembrane domains
> in 26 proteins. The prediction of SignalP and tmhmm are mostly consistent apart for Mycgr3|100022,
> which is predicted to contain one TM by SignalP, but none by tmhmm. Also, Mycgr3|100062 and Mycgr3|100559
> are predicted to contain both a signal peptide and transmembrane domains, suggesting that these proteins
> may enter the secretory pathway but are unlikely to be secreted.
> TargetP predicts 9 proteins with a putative signal
> peptide and 0 protein is predicted to be located in mitochondria. TargetP did not report Mycgr3|100062 as a protein entering the secretory pathway. In general, only SignalP and
> transmembrane domain (TMHMM) predictions are used in annotation pipelines.*


c) You used SignalP 4.0, tmhmm 2.0 and TargetP 2.0. Updates or new tools are regularly released and often lead to more accurate predictions. SignalP 6.0 and deepTMHMM 1.0 are newer versions of the tools you used and they are available online (https://services.healthtech.dtu.dk/services/SignalP-6.0/ and https://services.healthtech.dtu.dk/services/DeepTMHMM-1.0/).

Using the file **~/data/fungalgenomics\_collemare/day1/Mycgr3.100proteins.fasta**, run these tools with the online interface wiht parameters for Eukaryotes and short outputs.

Q3: For each tool, compare the results between the version you used and the later version. Are they all consistent?
Can you identify an example where different predictions could have a strong implication on the prediction of the sub-cellulare localization? How do you evaluate the accuracy of the different predictions?

> *Answer: SignalP 6.0 predicts 9 proteins with a signal peptide. Mycgr3|100062 was predicted to have a signal peptide with verison 4.0
> but not by TargetP, and a transmembrane domain was found by TMHMM. The results from 6.0 version appear unambiguous, and the previous predictiopn by version 4.0 was likely incorrect.
> DeepTMHMM 1.0 predicts 25 proteins with transmembrane domains, but the results are the same with TMHMM 2.0 for 23 proteins only.
> Mycgr3|100264 (2 TMs), Mycgr3|100498 (1 TM) and Mycgr3|100559 (1 TM) were predicted by TMHMM only, while Mycgr3_100383 (1 TM) and Mycgr3_100473 (2 TMs) were predicted by DeepTMHMM only. It is important to notice that Mycgr3|100559 is predicted to contain a signal peptide by both versions of SignalP, and thus predicting the presence or absence of a transmembrane domain has an important consequence on the prediction where this protein may be localized (secreted outside the cell or retained in a membrane).
> A more striking difference between TMHMM and DeepTMHMM is the number of predicted transmembrane domains. Out of 23, only 6 proteins
> (Mycgr3_100057, Mycgr3_100094, Mycgr3_100344, Mycgr3_100409, Mycgr3_100510 and Mycgr3_100550) are predicted with the same topology.
> The number of predicted transmembrane domains can vary greatly between the two tools, with the extreme case of Mycgr3_100515 in which TMHMM predicts 2 domains, but DeepTMHMM reports 10.
> In contrast to SignalP, there is no easy way to evaluate the accuracy of the transmembrane domain prediction. The precise position of these helices in the proteins should be considered very cautiously.*
