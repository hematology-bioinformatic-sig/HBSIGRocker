# xcmsrocker: Rocker image for metabolomics data analysis

Software and data is required for reproducible research. However, detailed workflows connecting software and data would be the key to reproducible research in metabolomics studies. Xcmsrocker is a linux based [rocker](https://www.rocker-project.org/)/docker image to host the workflow of [R based metabolomics software]((https://yufree.cn/en/2018/01/17/use-docker-to-package-your-metabolomics-study/)). It includes multiple mainstream R packages used in metabolomics study with RStduio as IDE. Such image could be deployed on single machine or [cluster(HPC or cloud computing)](https://yufree.cn/en/2022/05/26/using-xcmsrocker-on-hpc-via-singularity/). 

Besides, `rmwf` package is attached in this image to provide detailed workflow template( File - New File - R Markdown - From Template - Select template with {rmwf}) and facilitate the users to perform metabolomics data analysis and/or comparisons. Specifically, paired mass distances dependent analysis (PMDDA) and reactomics analysis templates could be found here.

If you preferred to perform Python code within RStudio through reticulate package, you might try [metaborocker](https://hub.docker.com/repository/docker/yufree/metaborocker).

You are welcome to contribute your new algorithm/software/workflow! Just PR!

Click [here](https://docs.google.com/presentation/d/1bVEbH_n6qjD9XH86hw7RFReb9ACdgEHwnYoD73ZmRSg/edit?usp=sharing) to check the poster for ASMS 2022.

## Reference

- Yu, M., Dolios, G., Petrick, L., 2022. Reproducible untargeted metabolomics workflow for exhaustive MS2 data acquisition of MS1 features. Journal of Cheminformatics 14, 6. https://doi.org/10.1186/s13321-022-00586-8

## Workflow template usage

1.  Install [Docker](https://www.docker.com/) and run Docker in your system

2.  Pull the Rocker image `docker pull yufree/xcmsrocker:latest`

3.  Use `docker run -e PASSWORD=xcmsrocker -p 8787:8787 yufree/xcmsrocker` to start the image

4.  Open the browser and visit <http://localhost:8787> or [http://[your-ip-address]:8787](http://%5Byour-ip-address%5D:8787) to power on RStudio server

5.  Default user name is `rstudio` and password is `xcmsrocker`

6.  Enjoy your data analysis! If you perferred to try PMDDA workflow, do the following step in RStudio:

-   Go to File - New File - Rmarkdown...
-   Click 'From Template'
-   Choose 'PMDDA Metabolomics Workflow' and click OK
-   You will see a Rmd file with PMDDA data analysis script.

Step 2-6 could be visualized:

![pmdda](https://raw.githubusercontent.com/yufree/yufree.cn/master/static/images/pmdda.gif)

## Packages

### Peak picking

-   [xcms](https://bioconductor.org/packages/release/bioc/html/xcms.html) Generate peaks list/EIC/diffreport
-   [x13cms](http://pubs.acs.org/doi/10.1021/ac403384n) global tracking of isotopic labels in untargeted metabolomics

### Improved Peak picking

-   [IPO](https://bioconductor.org/packages/release/bioc/html/IPO.html) For xcms peak picking optimazation
-   [Autotuner](https://bioconductor.org/packages/devel/bioc/vignettes/Autotuner/inst/doc/Autotuner.html) Automated parameter selection for untargeted metabolomics data processing
-   [xMSanalyzer](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-14-15) improved Peak picking for xcms and apLCMS

#### Comparison

-   IPO/Autotunner/default setting of xcms

-   Template

``` r
rmarkdown::draft("peakpicking.Rmd", template = "peakpicking", package = "rmwf")
```

#### For MS/MS

-   [decoMS2](https://pubs.acs.org/doi/10.1021/ac400751j) An Untargeted Metabolomic Workflow to Improve Structural Characterization of Metabolites
-   [msPurity](https://pubs.acs.org/doi/10.1021/acs.analchem.6b04358) Automated Evaluation of Precursor Ion Purity for Mass Spectrometry-Based Fragmentation in Metabolomics
-   [MetDIA](http://www.metabolomics-shanghai.org/softwaredetail.php?id=40) Targeted Metabolite Extraction of Multiplexed MS/MS Spectra Generated by Data-Independent Acquisition for SWATH

### Peak filter/visulization/workflow

-   [enviGCMS](https://cran.r-project.org/web/packages/enviGCMS/index.html) Filter peaks based on experimental design
-   [metaMS](https://www.ncbi.nlm.nih.gov/pubmed/24656939) An open-source pipeline for GC–MS-based untargeted metabolomics
-   [ChemoSpec](https://cran.r-project.org/web/packages/ChemoSpec/index.html) Exploratory Chemometrics for Spectroscopy

### Peak annotation/group/selection

-   [pmd](https://www.sciencedirect.com/science/article/pii/S0003267018313047) Select the independent peaks based on paired mass distance analysis
-   [CAMERA](https://bioconductor.org/packages/release/bioc/html/CAMERA.html) Annotation of peaklists generated by xcms, rule based annotation of isotopes and adducts, isotope validation, EIC correlation based tagging of unknown adducts and fragments
-   [RAMClustR](https://pubs.acs.org/doi/abs/10.1021/ac501530d) A feature clustering algorithm for non-targeted mass spectrometric metabolomics data
-   [mz.unity](http://pubs.acs.org/doi/abs/10.1021/acs.analchem.6b01702) Defining and Detecting Complex Peak Relationships in Mass Spectral Data
-   [Rdisop](https://bioconductor.org/packages/release/bioc/html/Rdisop.html) Decomposition of Isotopic Patterns
-   [InterpretMSSpectrum](https://pubs.acs.org/doi/10.1021/acs.analchem.6b02743) Annotate and interpret deconvoluted mass spectra (mass\*intensity pairs) from high resolution mass spectrometry devices
-   [classyfireR](https://cran.r-project.org/web/packages/classyfireR/index.html) Retrieve existing entity classifications from SMILES or InChls.

#### Comparison

-   CAMERA, RAMClustR, pmd, xMSannotator

-   Template

``` r
rmarkdown::draft("annotation.Rmd", template = "annotation", package = "rmwf")
```

### Batch correction

-   [Msprep](https://github.com/KechrisLab/MSPrep) Summarization, normalization and diagnostics for processing of mass spectrometry–based metabolomic data by Median, Quantile, Cross-Contribution Compensating Multiple Standard Normalization (CRMN), Surrogate Variable Analysis (SVA) and Removal of Unwanted Variation (RUV).
-   [BatchCorrMetabolomics](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4796354/) Improved batch correction in untargeted MS-based metabolomics by pool QC.

#### Comparison

-   Data with QCs/run order/batch information: loess, spline, ComBat

-   Data without QCs/run order/batch information: normalize to zero mean and unit variance,normalize to zero mean and squared root variance,normalize to zero mean but variance/SE,vast scaling,level scaling,total sum row,Median row,Mean row,PQN,VSN,Quantile,lumi rsn,Limma CyclicLoess,AFFA CUBICSpline,SVA,iSVA,PCR

-   Template

``` r
rmarkdown::draft("normalization.Rmd", template = "normalization", package = "rmwf")
```

### Peaks identification

-   [xMSannotator](http://pubs.acs.org/doi/abs/10.1021/acs.analchem.6b01214) MS1 annotation
-   [MetFragr](http://ipb-halle.github.io/MetFrag/projects/metfragr/) The R package enables functionalities from the MetFrag Commandline tool to be used within the R programming language.

### Omics

-   [xMWAS](https://www.ncbi.nlm.nih.gov/pubmed/29069296) a data-driven integration and differential network analysis tool.
-   [MetabNet](https://www.ncbi.nlm.nih.gov/pubmed/26125020) An R Package for Metabolic Association Analysis of High-Resolution Metabolomics Data.

### Statistical analysis

-   [caret](http://topepo.github.io/caret/index.html) general machine learning workflow for more than 200 models
-   [caretEnsemble](https://cran.r-project.org/web/packages/caretEnsemble/index.html) Functions for creating ensembles of caret models
-   [pROC](https://cran.r-project.org/web/packages/pROC/index.html) Tools for visualizing, smoothing and comparing receiver operating characteristic (ROC curves). (Partial) area under the curve (AUC) can be compared with statistical tests based on U-statistics or bootstrap. Confidence intervals can be computed for (p)AUC or ROC curves.
-   [gWQS](https://cran.r-project.org/web/packages/gWQS/index.html) Fits Weighted Quantile Sum (WQS) regressions for continuous, binomial, multinomial and count outcomes.
-   [UpSetR](https://cran.r-project.org/web/packages/UpSetR/index.html) A More Scalable Alternative to Venn and Euler Diagrams for Visualizing Intersecting Sets
-   [multcomp](https://cran.r-project.org/web/packages/multcomp/index.html) Simultaneous Inference in General Parametric Models to solve multiple comparisons issues
-   [h2o](https://docs.h2o.ai/h2o/latest-stable/h2o-docs/automl.html) Automating the machine learning workflow

### Chemometrics

-   [rcdk](https://cran.r-project.org/web/packages/rcdk/index.html) Interface to the 'CDK' Libraries
-   [ChemmineR](https://www.bioconductor.org/packages/devel/bioc/vignettes/ChemmineR/inst/doc/ChemmineR.html) Cheminformatics Toolkit for R
-   [webchem](https://github.com/ropensci/webchem) Chemical Information from the Web

### Reproducible research

-   [Risa](https://bioconductor.org/packages/release/bioc/html/Risa.html) Converting experimental metadata from ISA-tab into Bioconductor data structures
-   [rmwf](https://github.com/yufree/rmwf) Reproducilble Metabolomics WorkFlow(RMWF) is a R package for xcmsrocker. It will show the workflow templates and demo data for different R-based metabolomics software.

## Similar projects

- [Meta-Workflow](https://bookdown.org/yufree/Metabolomics/) will update every year to check new software and concepts in metabolomics

- For Java, you could select [MSDK](https://msdk.github.io/).

- For C/C++, you could select [OpenMS](https://www.openms.de/) or [ProteoWizard](http://proteowizard.sourceforge.net/).

- For C#, you could select [Prime](http://prime.psc.riken.jp/).

- For Matlab, you could select [Bioinformatics Toolbox](https://www.nature.com/protocolexchange/protocols/4347#).

- For python, you could select [emzed](http://emzed.ethz.ch/index.html) or [TinyMS](https://github.com/griquelme/tidyms)

### R 

Here is a nice [review](https://rformassspectrometry.github.io/metaRbolomics-book/) on R package for metabolomics.

- [patRoon](https://github.com/rickhelmus/patRoon) open source software platform for environmental mass spectrometry based non-target screening

- [MetaboAnalystR](https://github.com/xia-lab/MetaboAnalystR) R functions for MetaboAnalyst and they maintain [docker image](https://github.com/xia-lab/MetaboAnalyst_Docker) officially.

- [tidymass](https://www.tidymass.org/) the whole workflow of data processing and analysis for LC-MS-based untargeted metabolomics using tidyverse principles

- [R for Mass Spectrometry](https://www.rformassspectrometry.org/) R software for the analysis and interpretation of high throughput mass spectrometry assays.
