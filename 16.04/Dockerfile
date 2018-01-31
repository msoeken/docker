FROM ubuntu:16.04
MAINTAINER Mathias Soeken

RUN apt-get update
RUN apt-get install -y cmake git gcc g++ libgmp-dev libboost-all-dev libreadline-dev ninja-build zlib1g-dev

ENV HOME /root
WORKDIR /root

RUN git clone -b develop --recursive https://github.com/msoeken/cirkit
WORKDIR /root/cirkit

RUN mkdir build
WORKDIR /root/cirkit/build

RUN cmake -G Ninja -DCMAKE_CXX_COMPILER=g++-5 -DPYBIND11_PYTHON_VERSION=2.7 -Denable_cirkit-addon-reversible=ON -Dcirkit_ENABLE_PYTHON_API=ON ..
RUN ninja revkit revkit_python

WORKDIR /root

CMD ["bash"]
