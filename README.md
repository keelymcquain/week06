
# GA2 answers - `Keely McQuain`

## Part A: Starting a Git repository

### 1: Copy the template file and add your name

```bash
cp /fs/ess/PAS3493/share/GA2/GA2_template.md .
mv -v GA2_template.md README.md
```

### 2: Initialize a Git repository

### 3: Stage and commit README


## Part B: Exploring the GTF file with Unix data tools

### 4: Create `data`/`results` dirs and copy the GTF file

```bash
mkdir data 
mkdir results
cp /fs/ess/PAS3493/people/mcquain7/garrigos/ref/annot.gtf.gz /fs/ess/PAS3493/people/mcquain7/GA2/data/
```

The output of the command was:

```

```

### 5: File size of `annot.gtf.gz`

```bash
ls -lh
```

The output of the command was:

```
total 5.1M
-rw-rw----+ 1 mcquain7 PAS3493 5.1M Sep 26 16:35 annot.gtf.gz
```

### 6: Decompress the GTF file and check its size

```bash
gunzip data/annot.gtf.gz
```

```bash
ls -lh
```

The output of the command was:

```
total 123M
-rw-rw----+ 1 mcquain7 PAS3493 123M Sep 26 16:35 annot.gtf
```

*Answer*: The uncompressed file is approximately __24___ times larger.

### 7: Total number of lines in `annot.gtf`

```bash
wc -l annot.gtf
```

The output of the command was:

```
408402 annot.gtf
```

*Answer*: Total number of lines: __408,402___

### 8: Number of lines in the table section (header lines counted by eye)

```bash
head annot.gtf
```

The output of the command was:

```
#gtf-version 2.2
#!genome-build TS_CPP_V2
#!genome-build-accession NCBI_Assembly:GCF_016801865.2
#!annotation-source NCBI RefSeq GCF_016801865.2-RS_2022_12
NC_068937.1     Gnomon  gene    2046    110808  .       +       .       gene_id "LOC120427725"; transcript_id ""; db_xref "GeneID:120427725"; description "homeotic protein deformed"; gbkey "Gene"; gene "LOC120427725"; gene_biotype "protein_coding"; 
NC_068937.1     Gnomon  transcript      2046    110808  .       +       .       gene_id "LOC120427725"; transcript_id "XM_052707445.1"; db_xref "GeneID:120427725"; gbkey "mRNA"; gene "LOC120427725"; model_evidence "Supporting evidence includes similarity to: 25 Proteins"; product "homeotic protein deformed, transcript variant X3"; transcript_biotype "mRNA"; 
NC_068937.1     Gnomon  exon    2046    2531    .       +       .       gene_id "LOC120427725"; transcript_id "XM_052707445.1"; db_xref "GeneID:120427725"; gene "LOC120427725"; model_evidence "Supporting evidence includes similarity to: 25 Proteins"; product "homeotic protein deformed, transcript variant X3"; transcript_biotype "mRNA"; exon_number "1"; 
NC_068937.1     Gnomon  exon    52113   52136   .       +       .       gene_id "LOC120427725"; transcript_id "XM_052707445.1"; db_xref "GeneID:120427725"; gene "LOC120427725"; model_evidence "Supporting evidence includes similarity to: 25 Proteins"; product "homeotic protein deformed, transcript variant X3"; transcript_biotype "mRNA"; exon_number "2"; 
NC_068937.1     Gnomon  exon    70113   70962   .       +       .       gene_id "LOC120427725"; transcript_id "XM_052707445.1"; db_xref "GeneID:120427725"; gene "LOC120427725"; model_evidence "Supporting evidence includes similarity to: 25 Proteins"; product "homeotic protein deformed, transcript variant X3"; transcript_biotype "mRNA"; exon_number "3"; 
NC_068937.1     Gnomon  exon    105987  106087  .       +       .       gene_id "LOC120427725"; transcript_id "XM_052707445.1"; db_xref "GeneID:120427725"; gene "LOC120427725"; model_evidence "Supporting evidence includes similarity to: 25 Proteins"; product "homeotic protein deformed, transcript variant X3"; transcript_biotype "mRNA"; exon_number "4"; 
```

*Answer*: Number of header lines (counted by eye): __4___

*Answer*: Number of lines in the table section: __408,398___

### 9: Number of lines in the table section (`grep -v`)

```bash
grep -c -v "#" annot.gtf
```

The output of the command was:

```
408397
```

*Answer*: Number of lines in the table section: __408,397___

### 10: Count distinct sequences, save to `results/scaffolds.txt`

```bash
tail -n +5 annot.gtf | cut -f 1 | sort | uniq | wc -l
tail -n +5 annot.gtf | cut -f 1 | sort | uniq > /fs/ess/PAS3493/people/mcquain7/GA2/results/results.txt
```

The output of the command was:

```
168
```

*Answer*: Number of distinct sequences: __168___

### 11: Frequency table of feature types

```bash
tail -n +5 annot.gtf | cut -f 3 | sort | uniq -c
```

The output of the command was:

```
  1 ###
 141444 CDS
 166177 exon
  19673 gene
  25864 start_codon
  25892 stop_codon
  29347 transcript
```

### 12: Predict, then run `grep -c "gene"`

*Answer* (prediction, before running): a / **b** / c / d

I predict answer B is correct

```bash
grep -c "gene" data/annot.gtf
```

The output of the command was:

```
408397
```

*Answer*: Was your prediction correct, and what does the comparison with
the number of genes in your frequency table from question 11 tell you?

Yes, my predication was correct as the frequency table shows there's actually 19,673 genes, not 408,397.
## Part C: Updating your Git repository

### 13: Check Git status

```bash
git status
```

The output of the command was:

```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        data/
        results/

no changes added to commit (use "git add" and/or "git commit -a")
```

### 14: Create `.gitignore` and check status again

```bash
touch .gitignore
git add .gitignore
git status
```

The output of the command was:

```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   .gitignore

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

```

*Answer*: Is the `.gitignore` working as intended?
 
 Yes, it is working as intended.

### 15: Stage and commit `.gitignore`, then README again


## Part D: Exploring the FASTQ files with Unix data tools

### 16: Copy the FASTQ file

```bash
cp /fs/ess/PAS3493/people/mcquain7/garrigos/fastq/S63_R1.fastq.gz /fs/ess/PAS3493/people/mcquain7/GA2/data
```

The output of the command was:

```

```

### 17: Check Git status again

```bash
git status
```

The output of the command was:

```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

*Answer*: Does the FASTQ file show up? Why/why not?
No it does not. This is because it is in a directory that is being ignored by git. 

### 18: Number of reads in the FASTQ file

```bash
zcat S63_R1.fastq.gz | wc -l
```

The output of the command was:

```
2000000
```

*Answer*: Number of reads: __5,000,000___

### 19: Reads with at least 10 consecutive `N`s

```bash
zcat S63_R1.fastq.gz | grep -c "NNNNNNNNNN"
```

The output of the command was:

```
32612
```

*Answer*: Number of reads with at least 10 consecutive `N`s: __32,612___

### 20: Stage and commit README again

## Bonus

### 21: Why do the counts from questions 8 and 9 differ?

```bash
grep "#" annot.gtf
```

The output of the command was:

```
#gtf-version 2.2
#!genome-build TS_CPP_V2
#!genome-build-accession NCBI_Assembly:GCF_016801865.2
#!annotation-source NCBI RefSeq GCF_016801865.2-RS_2022_12
###
```

*Answer*: In question 8 when I visually counted the header lines, I used the command head, which only displayed the first 10 lines. By using grep in question 9, it located every line with a "#", not just the header lines. 

### 22: Concepts/commands you don't (fully) understand

*Answer*: I get confused when trying to use "../.." to navigate to files. I think it's easier for me to visually see the path typed out.  
I am also still a little confused on the purpose of git and committing files. 


## Created GitHub repo on 10/7
URL:  https://github.com/keelymcquain/week06 
