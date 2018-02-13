FROM ubuntu:17.10
MAINTAINER Mathias Soeken

RUN apt-get update
RUN apt-get install -y cmake git gcc g++ libgmp-dev libboost-all-dev libreadline-dev ninja-build zlib1g-dev build-essential devscripts pbuilder vim

ENV HOME /root
WORKDIR /root

RUN git clone -b develop --recursive https://github.com/msoeken/cirkit
WORKDIR /root/cirkit

COPY debian /root/cirkit/debian/
WORKDIR /root/
RUN tar -acf cirkit_2.4.orig.tar.gz cirkit

COPY sec.gpg /root/
COPY pub.gpg /root/

RUN gpg --import pub.gpg
RUN gpg --allow-secret-key-import --import sec.gpg

WORKDIR /root/cirkit

RUN debuild -S -sa

WORKDIR /root

RUN dput ppa:msoeken/ppa *.changes

CMD ["bash"]
