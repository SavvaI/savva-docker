FROM savvai/base:latest

WORKDIR /root
RUN git clone https://github.com/fdarmon/NeuralWarp
RUN conda config --append channels conda-forge
RUN conda create -n neural_warp --channel=conda-forge python=3.8
SHELL ["conda", "run", "--no-capture-output", "-p", "$CONDA_ROOT/envs/neural_warp", "/bin/bash", "-c"]
WORKDIR /root/NeuralWarp
RUN which pip
RUN pip install \
    imageio==2.9.0 \
    matplotlib==3.4.2 \
    numpy==1.21.2 \
    open3d==0.13.0 \
    opencv_python==4.5.3.56 \
    Pillow==8.4.0 \
    plotly==5.1.0 \
    pyhocon==0.3.58 \
    scikit_image==0.18.2 \
    scikit_learn==1.0.1 \
    scipy==1.7.1 \
    torch==1.9.0 \
    torchvision==0.10.0 \
    tqdm==4.62.3 \
    trimesh==3.9.26 \
    ninja==1.10.2

WORKDIR /root/
RUN git clone https://github.com/facebookresearch/pytorch3d.git
ENV CURDIR=/root/pytorch3d
WORKDIR $CURDIR
RUN git reset --hard 4046677cf1f8a6e5e9f9e8ef43e5c25200183c64
ENV MAX_JOBS=1
RUN wget https://github.com/NVIDIA/cub/archive/refs/tags/1.16.0.zip
RUN apt-get update && apt-get install -y --no-install-recommends unzip
RUN unzip 1.16.0.zip
ENV CUB_HOME=${CURDIR}/cub-1.16.0/
ENV FORCE_CUDA="True"
ENV NVCC_FLAGS="-DCUDA_HAS_FP16=1"
RUN pip install -e .