ARG BASE_CONTAINER=quay.io/condaforge/miniforge3
FROM $BASE_CONTAINER

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    # (TODO) A recommendation that comes along with 
    # build-essential is required to pip install finufft
    # && apt-get install -y --no-install-recommends \
    && apt-get install -y \
        build-essential \
        ssh \
        libfftw3-dev \
        pkg-config \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY environment.yml /tmp/

RUN mamba env update \
    --name "base" \
    --file /tmp/environment.yml \
    && \
    mamba clean --all -f -y
