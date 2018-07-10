
### Contamination
* [At least 7% of 1000 Genomes Project samples were contaminated with Mycoplasma.](https://biodatamining.biomedcentral.com/articles/10.1186/1756-0381-7-3)
* [About 11% of NCBI SRA rodent and primate RNA-Seq samples were contaminated with Mycoplasma.](https://academic.oup.com/nar/article/43/5/2535/2453278)
* Contamination detection should be performed before library construction to avoid a waste of time and money.
* Systematic contamination detection pipeline should also be performed once the data come back.

### Sequencing depth
* [Different library types require different sequencing depth.](https://www.nature.com/articles/nrg3642) New sequencing methods should be evaluated by saturation curve.
* [Sequencing depth also depends on the purpose.](https://www.nature.com/articles/nmeth.3152)
  * ENCODE recommends that each replicate of WGBS should have 30x coverage;
  * For DMR identification, sequencing at levels higher than 5-15x leads to wasted resources that would be better spent on an increased number of biological replicates.
  * If the goal is primarily to identify long DMRs with large methylation differences, 1-2x per sample is acceptable. 

### Quality control of enrichment
* [Lorenz curve](https://en.wikipedia.org/wiki/Lorenz_curve) can be used to evaluate the enrichment strength.
* For DNA-based enrichment, [deeptools](https://deeptools.readthedocs.io/en/develop/content/tools/plotFingerprint.html) can be used.
* For RNA-based enrichment, I have written a simple script to normalize different expression levels using the paired Input sample. Please refer to [MENG](https://dracarysking.github.io/MENG/) for more information.

### Different genome and annotation versions
* There are different reference assemblies for the same species. Be sure to use the currect one. Coordinates from different genome assemblies can be transformed using [LiftOver](https://genome.ucsc.edu/cgi-bin/hgLiftOver) or [CrossMap](http://crossmap.sourceforge.net/).
* There are also different sources of gene annotation, with [different sensitivity and specificity](https://genomebiology.biomedcentral.com/articles/10.1186/gb-2006-7-s1-s2).

### Statistics
* Simple fold change will lead to enrichment of lowly expressed genes because of their larger variances. Be sure to use statistics such as negative binomial distribution in [DESeq2](http://bioconductor.org/packages/devel/bioc/vignettes/DESeq2/inst/doc/DESeq2.html) to find the differences.

### Excel text format
* [Using Excel to store the final results with default format will affect at least 30 gene names which will be converted to date format and are irreversible.](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-5-80)


### OS dependent line breaks
* Dos uses `\r\n` for line breaks, while Linux uses '\n' for line breaks, which can lead to mistakes when files are transferred between different OS.
* `dos2unix` and `unix2dos` can be used easily to solve the problem.
