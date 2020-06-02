FROM continuumio/miniconda3:4.8.2

ARG DK_USER="dask"
ARG DK_UID="1100"
ARG DK_GID="1100"

ENV CONDA_DIR=/opt/conda \
    DK_USER=$DK_USER \
    DK_UID=$DK_UID \
    DK_GID=$DK_GID \
    HOME=/home/$DK_USER

RUN addgroup --gid $DK_GID $DK_USER && \
    adduser --disabled-password --gecos "Default user" -gid $DK_GID -uid $DK_UID $DK_USER && \    
    chown -R $DK_USER:$DK_GID $CONDA_DIR

USER $DK_USER

RUN conda update python

RUN conda install --yes \
    -c conda-forge \
    python-blosc \
    cytoolz \
    dask==2.14.0 \
    dask-ml \
    lz4 \
    nomkl \
    numpy==1.18.1 \
    pandas==1.0.1 \
    tini==0.18.0 \
    && conda clean --all \    
    && find /opt/conda/ -type f,l -name '*.a' -delete \
    && find /opt/conda/ -type f,l -name '*.pyc' -delete \
    && find /opt/conda/ -type f,l -name '*.js.map' -delete \
    && find /opt/conda/lib/python*/site-packages/bokeh/server/static -type f,l -name '*.js' -not -name '*.min.js' -delete \
    && rm -rf /opt/conda/pkgs

COPY prepare.sh /usr/bin/prepare.sh

ENTRYPOINT ["tini", "-g", "--", "/usr/bin/prepare.sh"]
