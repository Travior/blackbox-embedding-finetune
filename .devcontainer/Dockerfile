FROM nvidia/cuda:12.1.0-devel-ubuntu22.04

RUN apt update
RUN apt install -y build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev
RUN apt install -y nvidia-container-toolkit
RUN apt-get install -y lzma liblzma-dev libbz2-dev

RUN mkdir -p /temp/python
WORKDIR /temp/python
RUN wget https://www.python.org/ftp/python/3.12.1/Python-3.12.1.tgz
RUN tar -xf Python-3.12.1.tgz

WORKDIR /temp/python/Python-3.12.1
RUN ./configure --enable-optimizations
RUN make -j $(nproc)
RUN make altinstall

RUN rm -rf /temp/python

ADD extra /temp/extra
RUN pip3.12 install -r /temp/extra/requirements.txt
