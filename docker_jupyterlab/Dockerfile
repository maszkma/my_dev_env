FROM python:3.9

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y tzdata
ENV TZ=Asia/Tokyo

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y \ 
    python3-sklearn \
    python3-sklearn-lib \
    python3-llvmlite \
    libgl1-mesa-dev \
    wget \
    git \
    vim \
    curl \
    make \
    cmake \
    nodejs \
    npm


ADD requirements.txt .
RUN python -m pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt
RUN rm -rf ~/.cache/pip

RUN jupyter labextension install \
    @kiteco/jupyterlab-kite \
    @hokyjack/jupyterlab-monokai-plus \
    @ryantam626/jupyterlab_code_formatter \
    @jupyterlab/toc \
    @axlair/jupyterlab_vim \
    && jupyter serverextension enable --py jupyterlab_code_formatter

# install jupyter-kite
RUN cd && \
    wget https://linux.kite.com/dls/linux/current && \
    chmod 777 current && \
    sed -i 's/"--no-launch"//g' current > /dev/null && \
    ./current --install ./kite-installer

RUN apt-get autoremove -y \
    && apt-get clean \
    && rm -rf \
        /var/lib/apt/lists/* \
        /var/cache/apt/* \
        /usr/local/src/* \
        /tmp/*

WORKDIR "/home/work/"
