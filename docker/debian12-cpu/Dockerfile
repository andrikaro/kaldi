FROM arm64v8/debian:12
LABEL maintainer="jtrmal@apptek.com"

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        g++ \
        gfortran \
        make \
        automake \
        autoconf \
        bzip2 \
        unzip \
        wget \
        sox \
        libtool \
        git \
        python3 \
        zlib1g-dev \
        ca-certificates \
        patch \
        python-is-python3 && \
    rm -rf /var/lib/apt/lists/*


RUN git clone --depth 1 --branch osx-arm64 https://github.com/andrikaro/kaldi.git /opt/kaldi #EOL
RUN    cd /opt/kaldi/tools && \
       ./extras/install_openblas.sh  && \
       make -j 10 && \
       cd /opt/kaldi/src && \
       ./configure --shared --mathlib=OPENBLAS && \
       make depend -j $(nproc) && \
       make -j 10 

WORKDIR /opt/kaldi/
