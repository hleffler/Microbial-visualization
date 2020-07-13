# REU-microbial-visualization
This is for a project. These steps below must be done before attempting to run R scripts in Jupyter Notebook. 
<br>
# Kraken2 taxanomic annotation 

Kraken2 is a taxonomic classification system that uses short genomic substrings (k-mer) matches. The k-mer is matched within a query sequence with the lowest common ancestor of all genomes containing the exact k-mer. Kraken is fast and provides a taxa report for each sample. To read more about Kraken2 and install the tool visit github.com/DerrickWood/kraken2/wiki. 

This step is on Carbonate, a supercomputer, because the data set was too large to transfer to a Jetstream VM. It is possible to do this step on Jetstream, if a larger volume is requested and attached. This script will align reads against the kraken database to find the taxa. In this case, I am using sediment metagenome data sampled from hydrocarbon seepages in the Gulf of Mexico and identifying taxa families. Taxa identification is necessary to find species richness later for the rarefaction curve. Rarefaction curves are described later, after the taxa is identified and generated into a .csv table. 

## Installing kraken2 locally

Documentation available here, 
- https://github.com/DerrickWood/kraken2/wiki
- https://blogs.iu.edu/ncgas/2019/09/24/taxa-annotation-for-shotgun-sequenced-metagenomic-data/

### Input data

Metagenomic datasets. In this case the metagenomes were downloaded from NCBI's Sequence Read Archive (SRA) under the BioProject number PRJNA553005. There are seven sediment metagenomes under this BioProject.

## Running kraken2 command 

`kraken2 --db $KRAKEN_DB --use-names --report-zero-counts --paired "$f"_1.fq "$f"_2.fq --report "$f"_kraken_report`

Looking at the command above, the input samples are the forward and reverse read of the sample. Only one sample can be ran at a time using this command. In this case we had seven samples, so the command was run seven times. 

## Results from kraken2

This command will generate a report with the specified parameters (use-names, report-zero-counts, paired) for the sample as output. More information about Kraken2 parameters are described in the manual. The output, "$f"_kraken_report generates a table that looks like:

Sample Name | % of aligned reads | # of reads covered by clade | # of reads assigned to this taxa | rank code | NCBI Taxa ID
------------ | ------------- | ------------ | ------------- | ------------- | ------------- 
Content from cell 1 | Content from cell 2 | cell 3 | cell 4 | cell 5 | cell 6 
Content in the first column | Content in the second column | third | fourth | fifth | six 
Content in the first column | Content in the second column | third | fourth | fifth | six 
Content in the first column | Content in the second column | third | fourth | fifth | six 

Since every output is in a separate table, we need to combine them to make a rarefaction curve later. To prepare for this step, all kraken reports should be placed in thier own directory.

## Generating one output table for all the samples
Since the kraken reports currently are generated for each sample, we will need to generate one output csv or tsv table that has the taxanomic abundances for all the samples. The resulting table will be provides as input for the different visualization tools described in this notebook. 

### Download the python3 script from GitHub

`git clone https://github.com/npbhavya/Kraken2-output-manipulation.git`

### Place all the kraken2 reports to one directory

`mkdir kraken_report` 

`mv *_kraken_report FILEPATH/kraken_report/`

### Run the command

`python kraken-multiple-taxa.py -d kraken_report/ -r F -c 2 -o kraken-report-final`

## Result explained
The following command is used to get taxa information instead of taxa ID. The input -d for script the directory of kraken reports for each sample. 
-r defines taxonomic rank: (U)nclassified, (R)oot, (D)omain, (K)ingdom, (P)hylum, (C)lass, (O)rder, (F)amily, (G)enus, or (S)pecies
-c defines the column to be included in the final report col1: number of reads covered; col2: percentage of reads covered by taxa
-o output, defines output file name

The output is a table of taxa families followed by numbers that will look something like:

        Taxa    ['sample1', 'sample2', 'sample3', 'sample4', 'sample5', 'sample6', 'sample7']
        Pseudomonadaceae        ['78249', '103170', '81428', '76970', '75855', '69162', '92573']
        Moraxellaceae   ['9420', '6299', '10383', '10311', '6685', '3269', '9622']
        Enterobacteriaceae      ['31660', '27116', '34082', '31873', '24965', '16778', '33615']

This step was run again using a different rank (Phylum) and using percentages for the alluvial plot. kraken_reports_phylum.csv

### Converting the table to csv

`sed -e "s/\[//g;s/\]//g;s/'//g;s|\t|,|g" kraken-report-final >kraken_report_final_table.csv`

The output for the csv file command should look like a table. This table is now ready to be imported to use in R scripts in the Jupyter Notebook.
