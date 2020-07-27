# Microbial visualization
This is for a project. These steps below must be done before attempting to run R scripts in Jupyter Notebook. 
<br>
## Abstract

## How to install jupyter notebook
blogpost

## Kraken2 taxanomic annotation 

Kraken2 is a taxonomic classification system that uses short genomic substrings (k-mer) matches. The k-mer is matched within a query sequence with the lowest common ancestor of all genomes containing the exact k-mer. Kraken is fast and provides a taxa report for each sample. To read more about Kraken2 and install the tool visit github.com/DerrickWood/kraken2/wiki. 

### Installing kraken2 locally

Documentation available here, 
- https://github.com/DerrickWood/kraken2/wiki
- https://blogs.iu.edu/ncgas/2019/09/24/taxa-annotation-for-shotgun-sequenced-metagenomic-data/

### Running kraken2 command 

`kraken2 --db $KRAKEN_DB --use-names --report-zero-counts --paired "$f"_1.fq "$f"_2.fq --report "$f"_kraken_report`

Looking at the command above, the input samples are the forward and reverse read of the sample. Only one sample can be ran at a time using this command. In this case we had seven samples, so the command was run seven times. 

### Results from kraken2

Download the python3 script from GitHub

`git clone https://github.com/npbhavya/Kraken2-output-manipulation.git`

## Resources
input data is saved in input data folder
report issue for script 
paper
