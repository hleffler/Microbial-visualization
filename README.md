# Microbial visualization
This repository is for a project with [REU Jetstream](https://jetstream-cloud.org/research/reu.php) program. 

NCGAS

<br>
## Abstract
Metagenomes consist of the total genome content collected from an environmental sample containing bacterial, archaeal, and viral sequences present. These datasets are complex and can be overwhelming to visualize. Using multiple visualization methods benefits researchers by allowing them to perform exploratory analyses that could aid in downstream analysis of the data. This paper focuses on using different visualization methods including a rarefaction curve, ordination plots, alluvial plot and heatmap to represent a metagenomic dataset using Jetstream. Applying the visualization methods on a hydrocarbon seepage metagenomic dataset, we found that the samples cluster based on location, one sample was similar to both reference and seep samples, and the datasets had human contamination. These findings can now lead to potential downstream analysis questions to further assess this data. The scripts and input files used to create the different visualizations are available on GitHub.

## How to install Jupyter notebook
Jupyter notebook is a open-source project that allows code, text, images, and equations to be in one single document. To install Jupyter notebooks, follow [this blogpost](https://blogs.iu.edu/ncgas/2020/06/15/installing-jupyter-notebook-on-jetstream/).

## Kraken2 taxanomic annotation 

Kraken2 is a taxonomic classification system that uses short genomic substrings (k-mer) matches. The k-mer is matched within a query sequence with the lowest common ancestor of all genomes containing the exact k-mer. Kraken is fast and provides a taxa report for each sample. To read more about Kraken2 and install the tool visit github.com/DerrickWood/kraken2/wiki. 

### Install Kraken 2

Documentation available here 
- https://github.com/DerrickWood/kraken2/wiki
- https://blogs.iu.edu/ncgas/2019/09/24/taxa-annotation-for-shotgun-sequenced-metagenomic-data/


## Resources

All the input files used for the scripts to make the graphs is available in the [data_input](https://github.com/hleffler/Microbial-visualization/tree/master/input_data) folder.

To report an issue about the scripts please contact 

The paper written for this project can be located
