# adapted from https://github.com/Ecogenomics/GTDBTk/blob/80a48011f296db59c6fc5bc2d4e2ffae6ade0a0e/docker/Dockerfile

FROM ubuntu:16.04

ARG VER

# ---------------------------------------------------------------------------- #
# ------------------------ INSTALL PYTHON3, MUMMER --------------------------- #
# ---------------------------------------------------------------------------- #
RUN apt-get update -y -m && \
    # adds add-apt-repository command
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y software-properties-common && \
    # python ppa
    add-apt-repository -y ppa:deadsnakes/ppa && \

    apt-get update -y -m && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
                                               wget \
                                               libgomp1 \
                                               unzip \
                                               python3.8 \
                                               python3-setuptools \
                                               python3-wheel \
    # Fix ImportError: cannot import name 'sysconfig' from 'distutils' (/usr/lib/python3.8/distutils/__init__.py)
                                               python3.8-distutils \
                                               mummer=3.23~dfsg-3 && \

    # remove add-apt-repository
    DEBIAN_FRONTEND=noninteractive apt-get remove -y software-properties-common && \

    # Fix AttributeError: module 'platform' has no attribute 'linux_distribution'
    wget https://bootstrap.pypa.io/get-pip.py && \
    python3.8 get-pip.py && \
    rm get-pip.py && \

    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# ---------------------------------------------------------------------------- #
# ------------------------------ ALIAS PYTHON3  ------------------------------ #
# ---------------------------------------------------------------------------- #
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3.8 1 && \
    update-alternatives --set python /usr/bin/python3.8

# ---------------------------------------------------------------------------- #
# ----------------------------- INSTALL MASH --------------------------------- #
# ---------------------------------------------------------------------------- #
RUN wget https://github.com/marbl/Mash/releases/download/v2.0/mash-Linux64-v2.0.tar && \
    tar xf mash-Linux64-v2.0.tar && \
    mv mash-Linux64-v2.0/mash /usr/bin && \
    rm -r mash-Linux64-v2.0.tar mash-Linux64-v2.0

# ---------------------------------------------------------------------------- #
# ----------------------------- INSTALL FASTANI ------------------------------ #
# ---------------------------------------------------------------------------- #
RUN wget https://github.com/ParBLiSS/FastANI/releases/download/v1.32/fastANI-Linux64-v1.32.zip -q && \
    unzip fastANI-Linux64-v1.32.zip -d /usr/bin && \
    rm fastANI-Linux64-v1.32.zip

# ---------------------------------------------------------------------------- #
# --------------------------- INSTALL PIP PACKAGES --------------------------- #
# ---------------------------------------------------------------------------- #
RUN python -m pip install --upgrade pip && \
    python -m pip install drep==${VER} && \
    python -m pip cache purge

# ---------------------------------------------------------------------------- #
# ---------------------------- CREATE DATA DIR ------------------------------- #
# ---------------------------------------------------------------------------- #
RUN mkdir /data

# ---------------------------------------------------------------------------- #
# ---------------------------- SET THE ENTRYPOINT ---------------------------- #
# ---------------------------------------------------------------------------- #
ENTRYPOINT ["dRep"]
CMD ["-h"]
