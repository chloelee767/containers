# adapted from https://github.com/Ecogenomics/GTDBTk/blob/80a48011f296db59c6fc5bc2d4e2ffae6ade0a0e/docker/Dockerfile

FROM ubuntu:16.04

ARG VER

# ---------------------------------------------------------------------------- #
# --------------------- INSTALL HMMER, PYTHON3, PRODIGAL --------------------- #
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
                                               hmmer=3.1b2-2 \
                                               prodigal=1:2.6.2-2 \
                                               unzip \
                                               python3.8 \
                                               python3-setuptools \
                                               python3-wheel \
    # Fix ImportError: cannot import name 'sysconfig' from 'distutils' (/usr/lib/python3.8/distutils/__init__.py)
                                               python3.8-distutils && \

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
# ----------------------------- INSTALL PPLACER ------------------------------ #
# ---------------------------------------------------------------------------- #
RUN wget https://github.com/matsen/pplacer/releases/download/v1.1.alpha19/pplacer-linux-v1.1.alpha19.zip -q && \
    unzip pplacer-linux-v1.1.alpha19.zip && \
    mv pplacer-Linux-v1.1.alpha19/* /usr/bin && \
    rm pplacer-linux-v1.1.alpha19.zip && \
    rm -rf pplacer-Linux-v1.1.alpha19

# ---------------------------------------------------------------------------- #
# --------------------------- INSTALL PIP PACKAGES --------------------------- #
# ---------------------------------------------------------------------------- #
RUN python -m pip install --upgrade pip && \
    python -m pip install checkm-genome==${VER} && \
    python -m pip cache purge

# ---------------------------------------------------------------------------- #
# --------------------- SET CHECKM MOUNTED DIRECTORIES ---------------------- #
# ---------------------------------------------------------------------------- #
RUN mkdir /refdata && \
    mkdir /data && \
    checkm data setRoot /refdata

# ---------------------------------------------------------------------------- #
# ---------------------------- SET THE ENTRYPOINT ---------------------------- #
# ---------------------------------------------------------------------------- #
ENTRYPOINT ["checkm"]
CMD ["-h"]
