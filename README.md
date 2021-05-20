README
================
Rasmus Kirkegaard
20 May, 2021

# Test sequencing the Zymo mock community using “Q20EA” chemsitry by Oxford Nanopore

We were lucky to be offered to try the new “Q20” chemistry ahead of the
wide release. This post shows what the data looked like at the time we
got it and might not reflect the performance when the kit enters a wide
release as basecalling algorithms etc might have been fine tuned in the
meantime. The main selling point with this chemistry+bonito basecalling
was improved single pass accuracy. To evaluate the accuracy we sequenced
the zymo mock community where a known reference is available so it is
possible to determine how well the basecalled reads reflect the genomes.
The sequencing was carried out on the Promethion P24 platform with the
Zymo mock DNA directly from supplier without any pretreatment (no short
read elimination). The DNA fragments have a peak around 7 kbp but with a
tail of short fragments. To maximise yield the short fragments would
ideally have been removed but since the DNA material was limited I
omitted this as I figured that a Promethion Flowcell would anyway
generate plenty of data to check the quality of the reads for this low
complexity sample.

# DNA input size distribution

The DNA size distribution was checked using a genomic screentape.

![](data/Zymo_mock_size_distribution_genomic_screentape.jpg)

# Data availability

I have uploaded the basecalled data and the fast5 files to the ENA
[PRJEB43406](https://www.ebi.ac.uk/ena/browser/view/PRJEB43406).

# Basecalling with bonito (v. 0.3.5)

The reads were basecalled using bonito (v. 0.3.5) with a model
specifically trained for this new type of data.

## Overall alignment accuracy

The modal alignment accuracy (reported by bonito) seems to be better
than 99 % (Q20) from reading single DNA molecules!!! So the chemistry
clearly delivers excellent performance on accuracy.

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

## Alignment accuracy pr genome

Since the zymo includes a number of different organisms it would be
interesting to see if the performance was equally good for all
organisms. The alignment accuracy distributions seems indicate that the
basecalling is slightly better for some organisms than others. For many
of the organisms the peak of the distribution is slightly higher than 99
% but for e.g. Salmonella Enterica the performance seems to be a bit
lower. The models for basecalling are likely going to be improved before
a wide release but it is important to keep in mind that your favourite
pet organisms might have modifications that are not yet included in the
basecalling models and thus show lower performance.

![](README_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

# Genome assembly overview

While it is great to see improvements of the single read accuracy. It is
also interesting to see how the consensus accuracy is improving. To do
this I ran and assembly with metaflye (v. 2.8.3-b1695) inputting the
reads as –nano-corr and three of the chromosomes assembled into nice
circular contigs even with the “short” DNA fragments from the zymo
library. Here the assembly graph is visualised using bandage. I used the
three chromosomes for comparison

![](data/flye_nano_corr_assembly_graph.png)

## Lactobacillus fermentum

<table class=" lightable-paper lightable-striped" style="font-family: &quot;Arial Narrow&quot;, arial, helvetica, sans-serif; width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Bin.Id
</th>
<th style="text-align:left;">
\# contigs
</th>
<th style="text-align:left;">
Total length
</th>
<th style="text-align:right;">
Completeness
</th>
<th style="text-align:right;">
Contamination
</th>
<th style="text-align:left;">
MM100kb
</th>
<th style="text-align:left;">
Indel100kb
</th>
<th style="text-align:right;">
ANI
</th>
<th style="text-align:right;">
ANI Phred
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Lactobacillus\_fermentum
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
1905333
</td>
<td style="text-align:right;">
99.18
</td>
<td style="text-align:right;">
0.55
</td>
<td style="text-align:left;">
0.00
</td>
<td style="text-align:left;">
0.00
</td>
<td style="text-align:right;">
100.0000
</td>
<td style="text-align:right;">
Inf
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_1\_flye
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
1891256
</td>
<td style="text-align:right;">
98.72
</td>
<td style="text-align:right;">
0.55
</td>
<td style="text-align:left;">
16.87
</td>
<td style="text-align:left;">
1.96
</td>
<td style="text-align:right;">
99.9724
</td>
<td style="text-align:right;">
36
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_1\_flye\_racon2x\_raconILM
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
1890579
</td>
<td style="text-align:right;">
99.54
</td>
<td style="text-align:right;">
0.55
</td>
<td style="text-align:left;">
17.72
</td>
<td style="text-align:left;">
4.02
</td>
<td style="text-align:right;">
99.9721
</td>
<td style="text-align:right;">
36
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_1\_flye\_racon1x
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
1890853
</td>
<td style="text-align:right;">
98.45
</td>
<td style="text-align:right;">
0.55
</td>
<td style="text-align:left;">
18.03
</td>
<td style="text-align:left;">
7.46
</td>
<td style="text-align:right;">
99.9665
</td>
<td style="text-align:right;">
34
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_1\_flye\_racon2x
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
1890398
</td>
<td style="text-align:right;">
99.00
</td>
<td style="text-align:right;">
0.55
</td>
<td style="text-align:left;">
18.25
</td>
<td style="text-align:left;">
7.99
</td>
<td style="text-align:right;">
99.9662
</td>
<td style="text-align:right;">
34
</td>
</tr>
</tbody>
</table>

## Pseudomonas aeruginosa

<table class=" lightable-paper lightable-striped" style="font-family: &quot;Arial Narrow&quot;, arial, helvetica, sans-serif; width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Bin.Id
</th>
<th style="text-align:left;">
\# contigs
</th>
<th style="text-align:left;">
Total length
</th>
<th style="text-align:right;">
Completeness
</th>
<th style="text-align:right;">
Contamination
</th>
<th style="text-align:left;">
MM100kb
</th>
<th style="text-align:left;">
Indel100kb
</th>
<th style="text-align:right;">
ANI
</th>
<th style="text-align:right;">
ANI Phred
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Pseudomonas\_aeruginosa
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
6792330
</td>
<td style="text-align:right;">
99.68
</td>
<td style="text-align:right;">
0.61
</td>
<td style="text-align:left;">
0.00
</td>
<td style="text-align:left;">
0.00
</td>
<td style="text-align:right;">
100.0000
</td>
<td style="text-align:right;">
Inf
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_16\_flye\_racon2x\_raconILM
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
6792228
</td>
<td style="text-align:right;">
99.65
</td>
<td style="text-align:right;">
0.61
</td>
<td style="text-align:left;">
9.13
</td>
<td style="text-align:left;">
0.66
</td>
<td style="text-align:right;">
99.9929
</td>
<td style="text-align:right;">
49
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_16\_flye
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
6792141
</td>
<td style="text-align:right;">
99.68
</td>
<td style="text-align:right;">
0.61
</td>
<td style="text-align:left;">
9.13
</td>
<td style="text-align:left;">
1.13
</td>
<td style="text-align:right;">
99.9927
</td>
<td style="text-align:right;">
49
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_16\_flye\_racon2x
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
6791974
</td>
<td style="text-align:right;">
99.35
</td>
<td style="text-align:right;">
0.61
</td>
<td style="text-align:left;">
9.19
</td>
<td style="text-align:left;">
2.83
</td>
<td style="text-align:right;">
99.9900
</td>
<td style="text-align:right;">
46
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_16\_flye\_racon1x
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
6791962
</td>
<td style="text-align:right;">
99.68
</td>
<td style="text-align:right;">
0.61
</td>
<td style="text-align:left;">
9.22
</td>
<td style="text-align:left;">
3.06
</td>
<td style="text-align:right;">
99.9894
</td>
<td style="text-align:right;">
45
</td>
</tr>
</tbody>
</table>

## Staphylococcus aureus

<table class=" lightable-paper lightable-striped" style="font-family: &quot;Arial Narrow&quot;, arial, helvetica, sans-serif; width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Bin.Id
</th>
<th style="text-align:left;">
\# contigs
</th>
<th style="text-align:left;">
Total length
</th>
<th style="text-align:right;">
Completeness
</th>
<th style="text-align:right;">
Contamination
</th>
<th style="text-align:left;">
MM100kb
</th>
<th style="text-align:left;">
Indel100kb
</th>
<th style="text-align:right;">
ANI
</th>
<th style="text-align:right;">
ANI Phred
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Staphylococcus\_aureus
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
2718780
</td>
<td style="text-align:right;">
99.67
</td>
<td style="text-align:right;">
0.08
</td>
<td style="text-align:left;">
0.00
</td>
<td style="text-align:left;">
0.00
</td>
<td style="text-align:right;">
100.0000
</td>
<td style="text-align:right;">
Inf
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_61\_flye
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
2718703
</td>
<td style="text-align:right;">
99.67
</td>
<td style="text-align:right;">
0.08
</td>
<td style="text-align:left;">
0.37
</td>
<td style="text-align:left;">
0.74
</td>
<td style="text-align:right;">
99.9989
</td>
<td style="text-align:right;">
68
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_61\_flye\_racon2x\_raconILM
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
2718746
</td>
<td style="text-align:right;">
99.67
</td>
<td style="text-align:right;">
0.08
</td>
<td style="text-align:left;">
0.33
</td>
<td style="text-align:left;">
2.69
</td>
<td style="text-align:right;">
99.9968
</td>
<td style="text-align:right;">
57
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_61\_flye\_racon2x
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
2718521
</td>
<td style="text-align:right;">
99.42
</td>
<td style="text-align:right;">
0.08
</td>
<td style="text-align:left;">
0.55
</td>
<td style="text-align:left;">
7.80
</td>
<td style="text-align:right;">
99.9917
</td>
<td style="text-align:right;">
48
</td>
</tr>
<tr>
<td style="text-align:left;">
ctg\_61\_flye\_racon1x
</td>
<td style="text-align:left;">
1
</td>
<td style="text-align:left;">
2718506
</td>
<td style="text-align:right;">
99.67
</td>
<td style="text-align:right;">
0.08
</td>
<td style="text-align:left;">
0.77
</td>
<td style="text-align:left;">
8.50
</td>
<td style="text-align:right;">
99.9896
</td>
<td style="text-align:right;">
46
</td>
</tr>
</tbody>
</table>

# IDEEL analyses (<https://github.com/mw55309/ideel>)

### Lactobacillus fermentum - How many of the genes are full length?

To ensure that indel errors left from the nanopore data do not cause
genes to break we can compare the gene length with that of the best hit
to a reference gene. Most genes appear to have a length that is similar
to the best BLAST hit in the reference database indicated by a relative
gene length of 1.

![](README_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

### Pseudomonas aeruginosa - How many of the genes are full length?

To ensure that indel errors left from the nanopore data do not cause
genes to break we can compare the gene length with that of the best hit
to a reference gene. Most genes appear to have a length that is similar
to the best BLAST hit in the reference database indicated by a relative
gene length of 1.

![](README_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

### Staphylococcus aureus - How many of the genes are full length?

To ensure that indel errors left from the nanopore data do not cause
genes to break we can compare the gene length with that of the best hit
to a reference gene. Most genes appear to have a length that is similar
to the best BLAST hit in the reference database indicated by a relative
gene length of 1.

![](README_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->
