FROM --platform=amd64 ubuntu:18.04

LABEL maintainer="antiguru110894@gmail.com" version="0.0.0"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       build-essential \
       git \
       curl \
       ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN curl -L -o ~/miniconda.sh -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    && chmod +x ~/miniconda.sh \
    && ~/miniconda.sh -b -p /opt/conda \
    && rm -f ~/miniconda.sh 

ENV PATH /opt/conda/bin:$PATH
RUN activate base \
    && conda install python=3.8.5 -y

RUN git clone https://github.com/uber/causalml.git ~/causalml \
    && cd ~/causalml \
    && pip install -r requirements.txt \
    && python setup.py build_ext --inplace \
    && python setup.py install \
    && rm -fR ~/causalml

RUN activate base \
    && pip install --user \
       dask \
       pyarrow \
       category_encoders