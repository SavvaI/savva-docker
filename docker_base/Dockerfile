FROM nvidia/cuda:11.6.0-cudnn8-devel-ubuntu18.04

# Required for Geo-Neus (?)
RUN apt-get update && apt-get install -y --no-install-recommends \
    ffmpeg \
    libsm6 \
    libxext6 \
    apt-utils \
    psmisc \
    vim \
    tmux \
    unzip \
    build-essential

# Git is used for versioning in some of our experiments
RUN apt-get update && apt-get install -y --no-install-recommends git

# Wget is required to download conda installation script
RUN apt-get update && apt-get install -y --no-install-recommends wget

ENV CONDA_ROOT='/opt/anaconda3'
RUN wget -O /tmp/conda.sh https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh && \
    bash /tmp/conda.sh -p $CONDA_ROOT -b -u && \
    rm /tmp/conda.sh
ENV PATH=$CONDA_ROOT/bin:$PATH
RUN conda init bash
RUN pip install gdown