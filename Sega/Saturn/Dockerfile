# Prepare the build image
FROM ubuntu:latest

ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install depedencies
RUN apt-get update
RUN apt-get install -y git wget curl parallel
RUN apt-get install -y flex bison gcc g++ make cmake
RUN apt-get install -y autotools-dev automake-1.15 gpg mkisofs

WORKDIR /home
RUN git clone https://github.com/SaturnSDK/Saturn-SDK-GCC-SH2.git
WORKDIR /home/Saturn-SDK-GCC-SH2

ENV SRCDIR=/home/Saturn-SDK-GCC-SH2/source
ENV BUILDDIR=/home/Saturn-SDK-GCC-SH2/build
ENV TARGETMACH=sh-elf
ENV BUILDMACH=x86_64-pc-linux-gnu
ENV HOSTMACH=x86_64-pc-linux-gnu
ENV INSTALLDIR=/home/Saturn-SDK-GCC-SH2/toolchain
ENV SYSROOTDIR=$INSTALLDIR/sysroot
ENV ROOTDIR=/home/Saturn-SDK-GCC-SH2
ENV DOWNLOADDIR=/home/Saturn-SDK-GCC-SH2/download
ENV PROGRAM_PREFIX=saturn-sh2-

RUN ./build-elf.sh

WORKDIR /home
ENV SATURN_ROOT=/home/Saturn-SDK-GCC-SH2