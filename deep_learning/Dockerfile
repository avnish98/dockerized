FROM continuumio/anaconda3:2019.03

RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y \
        libpq-dev \
        build-essential \
        git \
        sudo \
        cmake zlib1g-dev libjpeg-dev xvfb libav-tools xorg-dev libboost-all-dev libsdl2-dev swig \
        unzip zip \
    && rm -rf /var/lib/apt/lists/*

RUN conda update -n base conda
RUN conda install -y \
        pandas \
        matplotlib \
        seaborn \
        scikit-learn \
        jupyterlab \
        theano 
RUN conda install -c conda-forge tensorflow keras tensorboard scipy

ARG username
ARG userid

ARG home=/home/${username}
ARG workdir=${home}/work/

RUN adduser ${username} --uid ${userid} --gecos '' --disabled-password \
    && echo "${username} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${username} \
    && chmod 0440 /etc/sudoers.d/${username}

WORKDIR ${workdir}
RUN chown ${username}:${username} ${workdir}

USER ${username}
WORKDIR ${workdir}