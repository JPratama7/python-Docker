# Use the official Python 3.9 image as a base
FROM python:3.9-slim

RUN apt update && apt upgrade && apt -y install poppler-utils ffmpeg libsm6 libxext6

WORKDIR /app

COPY "3.9/requirements.txt" .

RUN pip install --upgrade pip && pip install --no-cache-dir --upgrade $(cat requirements.txt)

COPY . .
