FROM ubuntu:16.04


RUN apt-get update
RUN apt-get -qq install -y \
git \
wget \
unzip \
build-essential \
time \
iputils-ping 

RUN apt-get -qq install -y \
 python \
 python-dev \
 python-numpy

RUN ln -s /usr/lib/python2.7/plat-*/_sysconfigdata_nd.py /usr/lib/python2.7/

RUN git clone git://github.com/glennhickey/progressiveCactus.git /progressiveCactus \
&& cd progressiveCactus \
&& git checkout tags/0.1 -b 0.1 \
&& git submodule update --init

RUN cd /progressiveCactus && ls -lahrt \
&& git clone https://github.com/robsyme/nf-annotate.git ./patches \
&& cp patches/patches/ktremote.patch submodules/kyototycoon/ \
&& cp patches/patches/ktulog.patch submodules/kyototycoon/ \
&& cp patches/patches/kyotocabinet-1.2.76-gcc6.patch submodules/kyotocabinet/ \
&& ls -lahrt


RUN cd /progressiveCactus/submodules/kyototycoon && patch < ktulog.patch && patch < ktremote.patch
RUN cd /progressiveCactus/submodules/kyotocabinet && patch < kyotocabinet-1.2.76-gcc6.patch

RUN ls -lahrt /progressiveCactus/

RUN cd /progressiveCactus/ && make

RUN mkdir /workspace
WORKDIR /workspace

RUN echo 'alias progressiveCactus="bash /progressiveCactus/bin/runProgressiveCactus.sh"' >> ~/.bashrc

ENV PYTHONPATH /usr/local/progressiveCactus/submodules
ENV PATH /bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/usr/local/progressiveCactus/bin:/usr/local/progressiveCactus/submodules/kentToolBinaries


