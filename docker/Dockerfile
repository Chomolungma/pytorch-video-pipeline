FROM nvcr.io/nvidia/deepstream:5.0-dp-20.04-base

RUN apt-get update && apt install --no-install-recommends -y \
    ca-certificates \
    python-gst-1.0 \
    wget

# allow GObject to find typelibs
ENV GI_TYPELIB_PATH /usr/lib/x86_64-linux-gnu/girepository-1.0/

# use conda to simplify some dependency managemeny
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh

ENV PATH /opt/conda/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/cuda-10.2/compat:${LD_LIBRARY_PATH}

RUN conda install -y -c conda-forge \
    pygobject

# Gstreamer debug output location
env GST_DEBUG_DUMP_DOT_DIR=/app/logs

RUN rm -rf /var/lib/apt/lists/* && \
    conda clean -afy

WORKDIR /app