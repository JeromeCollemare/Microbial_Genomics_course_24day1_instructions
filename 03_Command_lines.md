*Microbial genomics, Functional annotation, Day 1*

Command lines
===

**Exercise 1: annotation using similarity search**
 
Q3a: Execute a test BLAST search using the file on the server **~/data/fungalgenomics_collemare/day1/Mycgr3.100000.fasta**, which contains a single sequence, and save the results in a text file.
 
~~~
$ blastp -db uniprot_sprot.fasta -query Mycgr3.100000.fasta > blast_result1.txt
~~~
 
Q3c: Let’s start with the output format. Which argument can you use to
output the results in a tabular format? Test your command line with a
single sequence first and save the results in a file.
 
~~~
$ blastp -db uniprot_sprot.fasta -query Mycgr3.100000.fasta -outfmt 6 > blast_result2.txt
~~~

Q4: A fungal genome typically contains 10-12k genes. It is therefore not very handy to report several subject sequences for each protein and it is usually preferred to report the best hit only. Which argument can you use in the command line to report only the best hit per query sequence? Test your command line with a single sequence first and save the results in a file. Assess the result.
 
~~~
$ blastp -db uniprot_sprot.fasta -query Mycgr3.100000.fasta -max_target_seqs 1 -outfmt 6 > blast_result3.txt
~~~

b) Now that you are familiar with blast command lines, run a blast search for the first 30 annotated proteins of *Z. tritici*.
 
~~~
$ blastp -db uniprot_sprot.fasta -query Mycgr3.30proteins.fasta -max_target_seqs 1 -outfmt 6 > blast_result4.txt
~~~

Q5a: Open the result file. Do you have only one result per query sequence as expected? How many query sequences have more than one hit (use a simple bash command using cut, uniq and sort to calculate the numbers)?
 
~~~ 
$ cut -f1 blast_result4.txt | uniq -c | sort -r
~~~
 
Q5b: The different reported regions for a single query are high-scoring pairs (HSPs). Quite often, one HSP is more significant than others. For the annotation file, it is thus sensible to report only one HSP. Which argument can you use to limit the number of reported HSPs? Test your command line and save the results in a file. Check if the results meet your expectations.
 
~~~ 
$ blastp -db uniprot_sprot.fasta -query Mycgr3.30proteins.fasta -max_target_seqs 1 -max_hsps 1 -outfmt 6 > blast_result5.txt
~~~

Q5c: Open the result file. Do all proteins share similarity with proteins from the Swiss-Prot database? If not, is there another argument that you could use to keep only the most relevant hits (choosing an arbitrary threshold)? Test your command line to exclude the non-reliable results. What is the biological meaning when a protein does not share sequence similarity with any other sequence?

~~~
$ blastp -db uniprot_sprot.fasta -query Mycgr3.30proteins.fasta -max_target_seqs 1 -max_hsps 1 -evalue 0.001 -outfmt 6 > blast_result6.txt
~~~

** **

**Exercise 2: search for conserved domains**
 
Q1a: Execute a test HMMSCAN search with the minimum number of arguments and using the file **~/data/fungalgenomics\_collemare/day1/Mycgr3.100proteins.fasta** and PFAM database. Save the results in a text file (the run should last about one minute).
 
~~~
$ hmmscan -o day1_hmm_result1.txt Pfam-A.hmm Mycgr3.100proteins.fasta
~~~

Q2a: Which argument can you use to output the results in a tabular format? Test your command line and save the results in a file.
 
~~~
$ hmmscan --tblout day1_hmm_result2_tblout.txt -o day1_hmm_result2_main.txt Pfam-A.hmm Mycgr3.100proteins.fasta
~~~

Q2b: Which argument can you use to not include hits with low support? Test your command line and save the result in a file. You can try different arguments.
 
~~~
$ hmmscan -E 0.0001 --tblout day1_hmm_result3_tblout.txt -o day1_hmm_result3_main.txt Pfam-A.hmm Mycgr3.100proteins.fasta
~~~
or when using the PFAM database for example
~~~
$ hmmscan --cut_GA --tblout day1_hmm_result3_tblout.txt -o day1_hmm_result3_main.txt Pfam-A.hmm Mycgr3.100proteins.fasta
~~~
 
Q3: Execute a HMMSCAN search using the file **~/data/fungalgenomics\_collemare/day1/Mycgr3.100proteins.fasta** and the dbCAN database, and save the results in a text file

~~~
$ hmmscan -E 0.0001 --tblout day1_hmm_result4_tblout.txt -o day1_hmm_result4_main.txt dbCAN-fam.hmm Mycgr3.100proteins.fasta
~~~

** **

**Exercise 3: search for conserved motifs**
 
Q1: Execute the three searches with the minimum number of arguments and using the file **~/data/fungalgenomics\_collemare/day1/Mycgr3.100proteins.fasta**. Save the results in text files.

~~~
$ signalp Mycgr3.100proteins.fasta > day1_signalp.txt
$ tmhmm --short Mycgr3.100proteins.fasta > day1_tmhmm.txt
$ targetp -fasta Mycgr3.100proteins.fasta > day1_targetp.txt
~~~
