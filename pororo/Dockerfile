FROM nvidia/cuda:11.1.1-cudnn8-devel-ubuntu20.04 
# FROM pytorch/pytorch:1.9.0-cuda11.1-cudnn8-devel

WORKDIR /app

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul

RUN apt-get update && \
    apt-get install -y apt-utils \
    python3-dev \
    python3-pip \
    wget \
    git \
    gcc \
    build-essential \
    cmake \
    libpq-dev \
    libsndfile-dev \
    libboost-system-dev \
    libboost-thread-dev \
    libboost-program-options-dev \
    libboost-test-dev \
    libeigen3-dev \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libsndfile1-dev \
    libopenblas-dev \
    libfftw3-dev \
    libgflags-dev \
    libgoogle-glog-dev \
    libgl1-mesa-glx \
    libomp-dev

# 1. upgrade pip
RUN pip3 install --upgrade pip

RUN pip3 install \
    torch==1.9.1+cu111 \
    torchvision==0.10.1+cu111 \
    torchaudio==0.9.1 \
    -f https://download.pytorch.org/whl/torch_stable.html

# 2. install python-mecab-ko
RUN pip3 install -v python-mecab-ko

# 3. install pororo
RUN pip3 install pororo

# 4. install brainspeech
RUN pip3 install soundfile \
    pydub

# 5. install etc modules
RUN pip3 install -v librosa \
    kollocate \
    koparadigm \
    g2pk \
    fugashi \
    ipadic \
    romkan \
    g2pM \
    jieba \
    opencv-python \
    scikit-image \
    editdistance==0.5.3 \
    epitran==1.2 \
    fastdtw==0.3.4 \
    future \
    Pillow==7.2.0 \
    pinyin==0.4.0 \
    scikit-learn \
    scipy \
    SoundFile==0.10.2 \
    numba==0.48 \
    ko_pron

WORKDIR /app/external_lib

RUN git clone https://github.com/kpu/kenlm.git
WORKDIR /app/external_lib/kenlm/build
RUN cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_POSITION_INDEPENDENT_CODE=ON
RUN make
ENV KENLM_ROOT_DIR="/app/external_lib/kenlm/"

WORKDIR /app/external_lib
RUN git clone -b v0.2 https://github.com/facebookresearch/wav2letter.git
WORKDIR /app/external_lib/wav2letter/bindings/python
RUN pip3 install -e .

WORKDIR /app

RUN pip3 install jupyterlab
