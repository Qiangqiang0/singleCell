# singleCell

## 10x 

ref: https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/what-is-cell-ranger

### 1. intro 

* __cellranger mkfastq__ make raw to fastq

* __cellranger count__ takes FASTQ files from cellranger `mkfastq` and performs alignment, filtering, barcode counting, and UMI counting

* __cellranger aggr__ aggregates outputs from multiple runs of cellranger count, normalizing those runs to the same sequencing depth and then recomputing the feature-barcode matrices and analysis on the combined data.

* __cellranger reanalyze__ takes feature-barcode matrices produced by cellranger count or cellranger aggr and reruns the dimensionality reduction, clustering, and gene expression algorithms using tunable parameter settings.


### 2. pipeline

output of cellranger count: 

Feature-Barcode Matrices: 

Type	Description

Unfiltered feature-barcode matrix	Contains every barcode from fixed list of known-good barcode sequences. This includes background and cell associated barcodes.

Filtered feature-barcode matrix	Contains only detected cellular barcodes.

```bash
cellranger mkfastq \

#
cellranger count --id=normal \
	--transcriptome=$ref \
	--fastqs 

#libraryies.csv
#library_id,molecule_h5
#normal,/path/to/count/normal/outs/molecule_info.h5
#irradiated,/path/to/count/irradiated/outs/molecule_info.h5
cellranger aggr --id=aggr --csv=libraries.csv

cellranger reanalyze

```
## smart-seq