Inconsistency in large pharmacogenomic studies
==============================================


Abstract
--------

Cancer cell line studies have long been used to test efficacy of therapeutic agents and to explore genomic factors predictive of response. Two large-scale pharmacogenomic studies were published recently (CGP and CCLE); each assayed a panel of several hundred cancer cell lines for gene expression, copy number, genome sequence, and pharmacological response to multiple anti-cancer drugs. The resulting datasets present a unique opportunity to characterize mechanisms associated with drug response, with 471 cell lines and 15 drugs assayed in both. However, while gene expression is well correlated between studies, the measured pharmacologic drugs response is highly discordant. This poor correspondence is surprising as both studies assessed drug response using common estimators: the IC50 (concentration at which the drug inhibited 50% of the maximal cellular growth), and the AUC (area under the activity curve measuring dose response). For drugs screened in both studies, only one had a Spearman correlation coefficient in measured response greater than 0.6. Importantly these results are also reflected in inconsistent associations between genomic features and drug response. Although the source of inconsistencies in drug response measures between these two well-controlled studies remains uncertain, it makes drawing firm conclusions about response very difficult and has potential implications for using these outcome measures to assess gene-drug relationships or select potential anti-cancer drugs based on their reported results. Our findings suggest standardization of response measurement protocols in pharmacogenomic studies is essential before such studies can live up to their promise.
 

Citation
--------

To cite this work in publication, use

Inconsistency in large pharmacogenomic studies. Haibe-Kains B, El-Hachem N, Birkbak NJ, Jin AC, Beck AH, Aerts HJ, Quackenbush J. Nature. 2013 Dec 19;504(7480):389-93. doi: 10.1038/nature12831. Epub 2013 Nov 27. PMID: 24284626


Full Reproducibility of the Analysis Results
--------------------------------------------

We describe below how to fully reproduce the figures and tables reported in Haibe-Kains et al. submitted, 2013. We automated the analysis pipeline  so that minimal manual interaction  is required  to reproduce our results. To do this, one must simply:

1.  Set up the software environment

2.  Run the R scripts

3.  Generate the Supplementary Information


Set up the software environment
-------------------------------

We developed and tested our analysis pipeline using R running on linux and Mac OSX platforms. To mimic our software environment the following R packages should  be installed:

* R version  3.0.1 (2013-05-16), x86_64-unknown-linux-gnu

* Base packages: base, datasets, graphics, grDevices, grid, methods, parallel,  splines, stats, utils

* Other packages: amap 0.8-7, Biobase 2.20.0,  BiocGenerics 0.6.0,  colorspace 1.2-2, GSA 1.03, MASS 7.3-26,  plotrix 3.4-7, prodlim 1.3.7,  survcomp 1.10.0,  survival 2.37-4, vcd 1.2-13,  WriteXLS 2.3.1,  xtable 1.7-1

* Loaded  via a namespace (and not attached): bootstrap 2012.04-0, epibasix  1.3, KernSmooth 2.23-10,  rmeta  2.16, SuppDists 1.1-9, survivalROC  1.0.3,  tools 3.0.1

All these packages are available on CRAN (http://cran.r-project.org) or Bioconductor (http://www.bioconductor.org), except for jetset  which is available on the CBS website (http://www.cbs.dtu.dk/biotools/jetset/).

Run the following commands in a R session to install all the required  packages:

source("http://bioconductor.org/biocLite.R")

biocLite(c("AnnotationDbi", "affy", "affyio", "hthgu133acdf", "hthgu133afrmavecs", "hgu133plus2cdf", "hgu133plus2frmavecs", "org.Hs.eg.db", "genefu", "frma", "Hmisc", "vcd", "epibasix", "amap", "gdata", "WriteXLS", "xtable", "plotrix", "R.utils", "DBI", "GSA", "gplots"))

Note that you may need to install Perl (http://www.perl.org/get.html)  and  its module  Text::CSV  XS for the WriteXLS package to write xls file; once  Perl is installed  in your system, use  the  following command to install the Text::CSV  XS module  through  CPAN (http://www.cpan.org/modules/INSTALL.html):

cpan Text/CSV_XS.pm

The Vennerable R package is not available on CRAN and should be downloaded and installed using the following commands:

download.file(url="http://download.r-forge.r-project.org/src/contrib/Vennerable_3.0.tar.gz", destfile="Vennerable_3.0.tar.gz")
install.packages("Vennerable_3.0.tar.gz", repos=NULL, type="source")

Lastly, follow the instructions on the CBS website to properly install the jetset  package or use  the following commands in R:

download.file(url="http://www.cbs.dtu.dk/biotools/jetset/current/jetset_1.6.0.tar.gz", destfile="jetset_1.6.0.tar.gz")
install.packages("jetset_1.6.0.tar.gz", repos=NULL, type="source")

Once  the packages are installed, clone the cdrug repository to get all the R scripts. GSEA jar file (http://www.broadinstitute.org/gsea/msigdb/download_file.jsp?filePath=/resources/software/gsea2-2.0.14.jar) and the geneset collection (http://www.broadinstitute.org/gsea/msigdb/download_file.jsp?filePath=/resources/msigdb/4.0/c5.all.v4.0.entrez.gmt) should be downloaded from the broad website.

* CDRUG_foo.R: Script containing  the definitions of all functions  required  for the analysis pipeline.

* CDRUG_normalization_cgp.R: Script to curate, annotate and normalize  of CGP data. CDRUG normalization ccle.R Script to curate, annotate and normalize  of CCLE data. CDRUG normalization gsk.R Script to curate, annotate and normalize  of GSK data.

* CDRUG_format.R: Script to identify common cell lines, tissue types  and drugs  investigated both in CGP and CCLE.

* CDRUG_analysis.R: Script generating all the figures and tables reported in the manuscript.

* CDRUG_analysisbis.R: Script generating Figure 4 in the manuscript.

* CDRUG_analysisbis_gsk.R: Script comparing the IC50  measures between CGP,  CCLE and GSK.

* CDRUG_pipeine.R: Master  script running  all the scripts  listed above to generate the analysis re- sults.

* matching_cell_line_CCLE_CGP.csv: Curation  of cell line name to match  CGP and CCLE nomen- clatures.

* matching_tissue_type_CCLE_CGP.csv: Curation  of tissue type  name to match  CGP  and  CCLE nomenclatures.

* matching_cell_line_GSK_CCLE_CGP.csv: Curation  of cell line name to match  those of GSK with those of CGP and CCLE.

* matching_tissue_type_GSK_CCLE_CGP.csv: Curation  of tissue type name to match  those of GSK with those of CGP and CCLE.


All the files required  to run the automated analysis pipeline are now in place.  It is worth noting that  raw gene expression and  drug sensitivity  data  are  voluminous, please ensure that  at least
25GB of storage are available.


Run the R scripts
-----------------

Open  a terminal  window and  go to the CDRUG directory.  You can  easily  run the analysis pipeline either  in batch  mode  or in a R session. Before  running  the pipeline  you can  specify  the number of CPU cores you want to allocate to the analysis (by default  only 1 CPU core  will be used). To do so, open  the script CDRUG pipeline.R and update line #33:

nbcore <- 4

to allocate four CPU cores for instance.

To run the full pipeline in batch  mode,  simply type the following command:

R CMD BATCH CDRUG pipeline.R Rout &

The progress of the pipeline could be monitored  using the following command:

tail -f Rout

To run the full analysis pipeline in an R session, simply type the following command:

source("CDRUG pipeline.R")

Key messages will be displayed to monitor the progress of the analysis.

The analysis pipeline was developed so that  all intermediate analysis results are  saved in the directories data and  saveres. Therefore, in case of interruption, the user can rerun the pipeline which will restart where it stopped.
