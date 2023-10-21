# LR_metagenomics_tools
A repository with different scripts and function to aid into the conversion of different outputs from long reads taxnomic profilers into standard R objects

load_mmseqs_dir()
------------------

The load_mmseqs_dir() function reads Last Common Ancestor (LCA) output files from MMseqs2 and loads them into a data frame. The LCA output files must have been generated with the --tax-lineage 1 option.

**Usage**

```markdown
load_mmseqs_dir(dir.path, frag_thr=3, sup_thr=0.7)


**Arguments**

* `dir.path`: Path to the directory where the LCA output files are stored.
* `frag_thr`: Threshold for the number of proteins detected in a query read. Reads with fewer than frag_thr proteins detected will be filtered out.
* `sup_thr`: Threshold for the percentage of consensus proteins that have to be in a read to be assigned the taxonomy. Reads with fewer than sup_thr consensus proteins will be filtered out.

**Errors**

* If the `dir.path` does not exist, an error will be thrown.
* If the files in the `dir.path` are not .tsv files with the ending "_lca.tsv", an error will be thrown.
* If the `sup_thr` is not between 0 and 1, an error will be thrown.
* If the `frag_thr` is not an integer greater than 0, an error will be thrown.

**Example**

markdown
res.df <- load_mmseqs_dir("lca_files", frag_thr=5, sup_thr=0.9)


This would load all of the LCA output files in the `lca_files` directory into a data frame. The data frame would only include reads with 5 or more proteins detected and reads with 90% or more consensus proteins.

**Output**

The load_mmseqs_dir() function returns a data frame with the following columns:

* `rank`: The taxonomic rank of the read.
* `name`: The name of the taxon.
* `total_fragments`: The number of reads assigned to the taxon.
* `support`: The percentage of consensus proteins that are assigned to the taxon.
* `taxonomy`: The full taxonomy of the taxon.

The data frame is also pivoted so that each sample has its own column. The values in the sample columns are the number of reads assigned to the taxon in that sample.

**Additional notes**

* The load_mmseqs_dir() function uses the lapply() function to read the LCA output files in parallel. This can significantly improve the performance of the function for large datasets.
* The load_mmseqs_dir() function uses the dplyr package to manipulate the data frames. The dplyr package provides a number of functions that are optimized for performance.
* The load_mmseqs_dir() function uses the tidyr package to pivot the data frame. The tidyr package provides a number of functions for manipulating the形状of data frames.

