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

  && R -e "BiocManager::install(c('xcms','IPO','sva','WGCNA', 'KEGGREST', 'KEGGgraph', 'SSPA','Rdisop', 'qvalue', 'GlobalAncova', 'globaltest', 'siggenes', 'Rgraphviz','ChemmineR','metaMS', 'msPurity', 'mixOmics', 'fgsea', 'Rita','lumi','CompoundDb','MetaboAnnotation','MsBackendMgf','MsBackendMsp','genefilter','metapone','GSVA','limma','TCGAbiolinks','SummarizedExperiment'))" \
  && install2.r --error \
    RAMClustR \
    ChemoSpec \
    webchem \
    InterpretMSSpectrum \
    tcltk2 \
    ROCS \
    plotly \
    caret \ 
    caretEnsemble \
    pROC \
    gWQS \
    UpSetR \
    multcomp \
    isva \ 
    fs \
    keras \
    pins \
    table1 \
    flextable \
    torch \
    mlr3verse \
    ooplah \
    dictionar6 \
    reticulate \
  && R -e "install.packages(c("mlr3proba","mlr3extralearners"), repos = "https://mlr-org.r-universe.dev")" \
  && installGithub.r \
    rstudio/tfhub \
    rstudio/tfdatasets \
    yufree/enviGCMS \
    yufree/pmd \
    yufree/mzrtsim \
    yufree/rmwf \
  && rm -rf /tmp/downloaded_packages \
  && strip /usr/local/lib/R/site-library/*/libs/*.so \
  && python3 -m pip install --no-cache-dir --upgrade pip && \
    python3 -m pip install --no-cache-dir \ 
    tensorflow==2.11.* \
    tensorflow-hub \
    tensorflow-datasets \
    scipy \
    protobuf \
    requests \
    Pillow \
    h5py \
    pandas \
    pydot \
    torch_geometric \
    pqi \
    mygene \
    configparser \
    numpy \
    sklearn \
    tqdm \
    lifelines \
    matplotlib \
    captum \
    scipy \
  && python3 -m pip install --no-cache-dir torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu \
  && python3 -m pip install --no-cache-dir pyg_lib torch_scatter torch_sparse torch_cluster torch_spline_conv -f https://data.pyg.org/whl/torch-2.0.0+cpu.html 
