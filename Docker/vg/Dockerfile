# Dockerfile for a full vg build from source
FROM ubuntu:18.04

ARG vg_git_revision=master
ARG vg_git_url=https://github.com/vgteam/vg.git


RUN apt-get -qq update && apt-get -qq install -y \
    sudo \
    pv \
    pigz \
    bsdmainutils \
    build-essential \
    make \
    git \
    zlib1g-dev \
    rs \
    gdb \
    time \
    gawk

RUN git clone "$vg_git_url" /vg

RUN cd /vg && git fetch --tags origin && git checkout "$vg_git_revision" && git submodule update --init --recursive

RUN sed -i s/march=native/march=ivybridge/ deps/sdsl-lite/CMakeLists.txt
RUN . ./source_me.sh && make get-deps && CXXFLAGS=" -march=ivybridge " make -j$(nproc) && make static

RUN mkdir /workspace
WORKDIR /workspace

ENV PATH /vg/bin:$PATH
