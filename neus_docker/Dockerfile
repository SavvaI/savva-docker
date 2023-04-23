nFROM savvai/base:latest

WORKDIR /root
RUN git clone https://github.com/Totoro97/NeuS/
RUN conda config --append channels conda-forge
RUN conda create -n neus --channel=conda-forge python=3.8
SHELL ["conda", "run", "--no-capture-output", "-p", "$CONDA_ROOT/envs/neus", "/bin/bash", "-c"]
WORKDIR /root/NeuS
RUN which pip
RUN pip install \
    trimesh==3.9.8 \
    numpy==1.19.2 \
    pyhocon==0.3.57 \
    icecream==2.1.0 \
    opencv_python==4.5.2.52 \
    tqdm==4.50.2 \
    torch==1.8.0 \
    scipy==1.7.0 \
    PyMCubes==0.1.2