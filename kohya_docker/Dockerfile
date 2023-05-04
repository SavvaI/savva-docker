FROM savvai/base:latest

WORKDIR /root
RUN git clone https://github.com/kohya-ss/sd-scripts.git
RUN conda config --append channels conda-forge
RUN conda create -n kohya-ss -y --channel=conda-forge python=3.10.6
SHELL ["conda", "run", "--no-capture-output", "-p", "$CONDA_ROOT/envs/kohya-ss", "/bin/bash", "-c"]

WORKDIR /root/sd-scripts
RUN pip install torch==1.12.1+cu116 torchvision==0.13.1+cu116 --extra-index-url https://download.pytorch.org/whl/cu116
RUN pip install --upgrade -r requirements.txt
ENV TORCH_CUDA_ARCH_LIST=6.0
RUN git clone https://github.com/facebookresearch/xformers
WORKDIR /root/sd-scripts/xformers
RUN git submodule update --init --recursive
RUN git reset --hard faa88b123514562dbe8e32ec72a25937b0dd9da5
RUN rm -rf ./build && \
    export TORCH_CUDA_ARCH_LIST=6.0 && \
    export FORCE_CUDA=1 && \
    python3 setup.py install && \
    pip install -v ./
WORKDIR /root/sd-scripts



