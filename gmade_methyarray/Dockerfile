FROM rocker/verse:latest
MAINTAINER "Yanhua Zheng" zyh3084989256@gmail.com
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    libnetcdf-dev \
    ## rgl support
    libgl1-mesa-dev \
    libglu1-mesa-dev \
    ## tcl tk support
    tcl8.6-dev \
    tk8.6-dev \
    ## python-env && pip3 support
    python3.10-venv \
    python3-pip
RUN R -e "BiocManager::install(c( 'KEGGREST', 'KEGGgraph', 'Rgraphviz','ChemmineR','metaMS', 'msPurity', 'mixOmics', 'fgsea', 'Rita','lumi','genefilter','metapone','GSVA','limma','TCGAbiolinks','SummarizedExperiment','methylationArrayAnalysis','rnaseqGene','simpleSingleCell','arrays','chipseqDB'))" 
RUN install2.r --error \
    ROCS \
    plotly \
    caret \ 
    caretEnsemble \
    pROC \
    isva \ 
    fs \
    pins \
    table1 \
    flextable \
    mlr3verse \
    ooplah \
    dictionar6 \
    reticulate
RUN installGithub.r \
    mlr-org/mlr3proba \
    mlr-org/mlr3extralearners@*release 
RUN rm -rf /tmp/downloaded_packages 
RUN strip /usr/local/lib/R/site-library/*/libs/*.so 
