# FROM python:3.10.6
# FROM nvidia/cuda:11.6.2-base-ubuntu20.04 AS build-stage
FROM nvidia/cuda:12.3.1-devel-ubuntu20.04

# Install Python
RUN apt-get update && DEBIAN_FRONTEND=noninteractive \
    apt-get install -y software-properties-common && \
    DEBIAN_FRONTEND=noninteractive add-apt-repository -y ppa:deadsnakes/ppa && \
    apt-get install -y python3.10 curl && \
    curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10

RUN curl -sSL https://install.python-poetry.org | python3.10 - --preview
RUN pip3 install --upgrade requests
RUN ln -fs /usr/bin/python3.10 /usr/bin/python

# LLM specific binaries
RUN apt-get update && \
    apt-get install -y build-essential && \
    apt-get install -y libgl1 && \
    apt-get install -y poppler-utils && \
    apt install -y libpython3.10-dev &&\ 
    apt install -y python3.10-distutils && \
    apt-get install -y libcairo2-dev pkg-config python3-dev && \
    apt-get install -y libtesseract-dev && \
    apt-get install -y tesseract-ocr


WORKDIR /app

COPY requirements.txt .

ENV CMAKE_ARGS="-DLLAMA_CUBLAS=ON"
RUN python -m pip install --no-cache-dir -r requirements.txt

COPY . .

# CMD ["python", "-m", "main"]
CMD ["/bin/bash"]