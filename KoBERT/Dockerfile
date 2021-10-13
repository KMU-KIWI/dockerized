FROM nvidia/cuda:11.1.1-cudnn8-runtime-ubuntu20.04

RUN apt-get update && DEBIAN_FRONTEND="noninteractive" apt-get install -y \
    tzdata

RUN apt-get install -y \
    python3 \
    python3-pip \
    git \
    curl \
    cmake \
    libprotobuf-dev \
    protobuf-compiler \
    python3-pybind11 \
    build-essential \
    pkg-config \
    libgoogle-perftools-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache \
    tensorflow \
    pandas \
    matplotlib \
    pandas \
    jupyterlab \
    torch==1.9.1+cu111 \
    torchvision==0.10.1+cu111 \
    torchaudio==0.9.1 \
    -f https://download.pytorch.org/whl/torch_stable.html

CMD ["/bin/bash", "-c", "jupyter lab --allow-root --port 8888 --ip=* --no-browser"]
