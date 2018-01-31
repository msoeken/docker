FROM ubuntu:14.04
MAINTAINER Mathias Soeken

RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:ubuntu-toolchain-r/test
RUN apt-get update
RUN apt-get install -y cmake3 git gcc-5 g++-5 libgmp-dev libboost-all-dev libreadline-dev ninja-build

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
