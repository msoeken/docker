FROM ubuntu:14.04
MAINTAINER Mathias Soeken

RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:ubuntu-toolchain-r/test
RUN apt-get update
RUN apt-get install -y cmake3 git gcc-5 g++-5 libgmp-dev libboost-all-dev libreadline-dev ninja-build build-essential devscripts pbuilder vim

ENV HOME /root
WORKDIR /root

RUN git clone -b develop --recursive https://github.com/msoeken/cirkit
WORKDIR /root/cirkit

RUN mkdir build
WORKDIR /root/cirkit/build
RUN cmake -G Ninja -DCMAKE_CXX_COMPILER=g++-5 -Denable_cirkit-addon-reversible=ON -DPYBIND11_PYTHON_VERSION=2.7 -DBUILD_TESTING=OFF -Dcirkit_ENABLE_PYTHON_API=ON -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_PYTHON_SITE_PATH=/usr/lib/python2.7/dist-packages ..
RUN ninja cirkit cirkit_python revkit revkit_python
RUN cmake -P cmake_install.cmake

WORKDIR /root

CMD ["bash"]
