FROM --platform=linux/amd64 python:3.9-slim-buster

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    curl \
    software-properties-common \
    git \
    libpq-dev \
    gcc \
    libgl1-mesa-glx \
    libglib2.0-0 \
    wget \
    tar \
    xz-utils \
    build-essential \
    cmake \
    libnss3 \
    libnss3-dev \
    libcairo2-dev \
    libjpeg-dev \
    libgif-dev \
    cmake \
    libblkid-dev \
    e2fslibs-dev \
    libboost-all-dev \
    libaudit-dev \
    libopenjp2-7-dev \
    g++ \
    && rm -rf /var/lib/apt/lists/*

RUN wget https://poppler.freedesktop.org/poppler-21.09.0.tar.xz \
    && tar xf poppler-21.09.0.tar.xz \
    && cd poppler-21.09.0 \
    && mkdir build \
    && cd build \
    && cmake -DCMAKE_BUILD_TYPE=Release \
             -DCMAKE_INSTALL_PREFIX=/usr \
             -DTESTDATADIR=$PWD/testfiles \
             -DENABLE_UNSTABLE_API_ABI_HEADERS=ON \
             .. \
    && make \
    && make install

WORKDIR /app

RUN apt remove g++ gcc cmake libnss3-dev libcairo2-dev libjpeg-dev libgif-dev libblkid-dev e2fslibs-dev libboost-all-dev libaudit-dev libopenjp2-7-dev -y

COPY ./* .

RUN pip3 install -r ./requirements.txt

EXPOSE 8501