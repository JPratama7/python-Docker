# Use the official Python 3.9 image as a base
FROM --platform=linux/amd64 python:3.9-slim

RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    postgresql-client \
    gcc \
    libgl1-mesa-glx \
    libglib2.0-0 \
    wget \
    tar \
    xz-utils \
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
    libopenjp2-7-dev g++

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

COPY "3.9/requirements.txt" .

RUN pip install --upgrade pip && pip install --no-cache-dir --upgrade $(cat requirements.txt)

COPY . .
