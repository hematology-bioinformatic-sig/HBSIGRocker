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
    python3-pip &&\
    install2.r --error pak &&\
    R -e "pak::repo_add(rhub = 'https://r-hub.r-universe.dev')" &&\
    R -e "pak::repo_add(mlrorg = 'https://r-hub.r-universe.dev')" &&\
    R -e "pak::pkg_install(c('tidyverse','blogdown','bookdown','tinytex','xcms','WGCNA', 'KEGGREST', 'KEGGgraph', 'plotly','pROC','sva','limma','fs','keras','tensorflow','pins','flextable','torch','mlr3verse','R6','reticulate', 'GSVA','graphite','clusterProfiler','igraph','ggraph','TCGAbiolinks','SummarizedExperiment', 'ggpubr','data.table','mlr3proba'),upgrade = TRUE,ask= FALSE, dependencies = NA)"  &&\
    R -e "pak::pkg_install(c('rstudio/tfhub','rstudio/tfdatasets','yufree/enviGCMS','yufree/pmd','mlr-org/mlr3extralearners@*release','hrbrmstr/hrbrthemes','immunogenomics/harmony','rainoffallingstar/erebor'),upgrade = TRUE,ask= FALSE, dependencies = NA)" &&\
   R -e "tinytex::install_tinytex(force = TRUE)" &&\
    R -e "tinytex::tlmgr_repo('http://mirrors.tuna.tsinghua.edu.cn/CTAN/')" &&\
    rm -rf /tmp/downloaded_packages && \
    R -e "pak::cache_clean()" &&\
    strip /usr/local/lib/R/site-library/*/libs/*.so 
