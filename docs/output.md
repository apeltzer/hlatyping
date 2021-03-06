# nf-core/hlatyping
Precision HLA typing from next-generation sequencing data.

This document describes the output produced by the pipeline.

## Pipeline overview
The pipeline is built using [Nextflow](https://www.nextflow.io/)
and processes data using the following steps:

* [OptiType](#optitype) - HLA genotyping based on integer linear programming 

## OptiType
[OptiType](https://github.com/FRED-2/OptiType) is an HLA genotyping algorithm based on linear integer programming. It provides accurate 4-digit HLA genotyping predictions from NGS data.
For further reading and documentation see the [OptiType documentation](https://github.com/FRED-2/OptiType).

The pipeline results contain a CSV file with the predicted HLA genotype. Each line contains one solution with the predicted HLA alleles in 4-digit nomenclature, the number of reads that are covered by this solution and the objective function value. If the number of enumerations (--enumerate N) is higher than 1, the CSV file will contain the optimal and sub-optimal solutions. 

```
    A1  A2  B1  B2  C1  C2  Reads   Objective
0   A*01:01 A*01:01 B*08:01 B*57:01 C*07:01 C*06:02 1127.0  1106.7139999999997
```
Additionally, a coverage plot of the predicted HLA genotype is produced for quality control purposes (see below). The coverage plot shows the amount of reads that cover every position of the selected HLA allele sequence. Further, the color encoding denotes if reads are paired or unpaired, contain mismatches, and if the matches are unique or ambiguous. In case of homozygous solutions, the coverage plot of the corresponding HLA allele will be shown once.

![coverage_plot](images/sample_coverage_plot.png)

**Output directory: `results/{timestamp}`**

* `{prefix}_{timestamp}_result.tsv`
  * TSV file, containing the predicted optimal (anf if enumerated, sub-optimal) HLA genotype. 
* `{prefix}_{timestamp}_coverage_plot.pdf`
  * pdf file, containing a coverage plot of the predicted alleles
