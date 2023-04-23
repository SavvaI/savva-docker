FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04

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
RUN apt-get update && apt-get install -y --no-install-recommends wget
RUN apt-get install -y python3-pip
RUN ln -s /usr/bin/python3 /usr/bin/python && \
    ln -s /usr/bin/pip3 /usr/bin/pip
RUN which python 
RUN which pip
RUN apt-get update && apt-get install -y --no-install-recommends \ 
    freeglut3-dev \
    sudo \
    lsb-release
    
RUN pip install gdown

WORKDIR /root
RUN git clone https://github.com/facebookresearch/pifuhd

WORKDIR /root/pifuhd

RUN pip install --upgrade pip setuptools wheel
    
RUN pip install \
    torch==1.5.0+cu101 torchvision==0.6.0+cu101 -f https://download.pytorch.org/whl/torch_stable.html \
    Pillow \
    scikit-image \
    tqdm \
    opencv-python \
    trimesh \
    PyOpenGL \
    ffmpeg
    
RUN git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose

RUN cd openpose/scripts/ubuntu && \
    chmod +x install_deps.sh && \
    sudo ./install_deps.sh 
    
RUN wget https://github.com/Kitware/CMake/releases/download/v3.26.3/cmake-3.26.3-linux-x86_64.sh -P /opt/
RUN chmod +x /opt/cmake-3.26.3-linux-x86_64.sh
RUN mkdir /opt/cmake-3.26.3-linux-x86_64/
RUN sudo bash /opt/cmake-3.26.3-linux-x86_64.sh --skip-license --prefix=/opt/cmake-3.26.3-linux-x86_64/
RUN sudo ln -s /opt/cmake-3.26.3-linux-x86_64/bin/* /usr/local/bin
RUN ls /opt/cmake-3.26.3-linux-x86_64/bin/
RUN cmake --version

ENV TZ=Europe/Moscow
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN sudo apt-get install -y --no-install-recommends libopencv-dev 
RUN cd openpose && \
    mkdir build/ && \
    cd build/ && \
    cmake -DCUDA_ARCH=Manual -DCUDA_ARCH_BIN="60" -DCUDA_ARCH_PTX="60" ..

RUN cmake --version
RUN cd openpose/build/ && \
    make -j5 
    
RUN ls openpose/build/