# GenEpi
GenEpi is a package to uncover epistasis associated with phenotypes by the machine learning approach, developed by Yu-Chuan Chang at [c4Lab](http://bioinfo.bime.ntu.edu.tw/c4lab/) of National Taiwan University.

<img src="https://github.com/Chester75321/GenEpi/raw/master/GenEpi.png" width="75%" height="75%">

The architecture and modules of GenEpi.

## Getting Started
### Installation
```
$ pip install GenEpi
```
>**NOTE:** GenEpi is a memory-consuming package, which might causes memory errors when calculating the epistasis of a gene containing a large number of SNPs. We recommend that the memory for running GenEpi should be over 256 GB.

### Inputs
**1\. Genotype Data:**

GenEpi takes the [Genotype File Format](http://www.stats.ox.ac.uk/~marchini/software/gwas/file_format_new.html) (.GEN) used by Oxford statistical genetics tools, such as IMPUTE2 and SNPTEST as the input format for genotype data. If your files are in [PLINK format](https://www.cog-genomics.org/plink/1.9/formats) (.BED/.BIM/.FAM) or [1000 Genomes Project text Variant Call Format](https://www.cog-genomics.org/plink/1.9/formats#vcf) (.VCF), you could use [PLINK](https://www.cog-genomics.org/plink/1.9/) with the following command to convert the files to the .GEN file.

If your files are in the **.BED/.BIM/.FAM** format.
```
$ plink --bfile prefixOfTheFilename --recode oxford --out prefixOfTheFilename
```
If your files is in the **.VCF** format.
```
$ plink --vcf filename.vcf --recode oxford --out prefixOfTheFilename
```

**2\. Phenotype & Environmental Factor Data**

GenEpi takes the .csv file without header line as the input format for phenotype and environmental factor data. The last column of the file would be considered as the phenotype data and the other columns would be considered as the environmental factor (covariates) data.
>**NOTE:** The order of the phenotype data should be same as the .GEN file.

## Usage example
### Running a test
We provided an [example script](https://github.com/Chester75321/GenEpi/tree/master/genepi/example/example.py) in [example folder](https://github.com/Chester75321/GenEpi/tree/master/genepi/example). Please use the following command for running a quick test.
```
$ python example.py
```

### Applying on your data
You may use this example script as a recipe and modify the input file names in Line 14 and 15 for running your data.
```python
str_inputFileName_genotype = "../sample.gen" # full path of the .GEN file.
str_inputFileName_phenotype = "../sample.csv" # full path of the .csv file.
```

### Options
For changing the build of USCS genome browser, please modify the parameter of the step one:
```python
genepi.DownloadUCSCDB(str_hgbuild="hg38") # for example: change to build hg38.
```
You could modify the threshold for Linkage Disequilibrium dimension reduction in the step two:
```python
genepi.EstimateLDBlock(str_inputFileName_genotype, float_threshold_DPrime=0.8, float_threshold_RSquare=0.8)
#default: float_threshold_DPrime=0.9 and float_threshold_RSquare=0.9
```

## Interpreting the Results
### The main table
GenEpi will automatically generate three folders (snpSubsets, singleGeneResult, crossGeneResult) beside your .GEN file. You could go to **crossGeneResult** directly to obtain your main table for episatasis in **Result.csv**

## Meta
Chester (Yu-Chuan Chang) - chester75321@gmail.com  
Distributed under the MIT license. See ``LICENSE`` for more information.  
[https://github.com/Chester75321/GenEpi/](https://github.com/Chester75321/GenEpi/)
