FROM ubuntu:xenial

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN apt-get update \
	&& apt-get install -y ca-certificates \
	&& apt-get install -y build-essential wget curl m4 make cmake \
	gfortran perl patch pkg-config bzip2 libglib2.0-0 libxext6 libsm6 libxrender1 \
    git mercurial subversion
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/archive/Anaconda2-4.4.0-Linux-x86_64.sh -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /opt/conda && \
    rm ~/anaconda.sh
RUN apt-get install -y grep sed dpkg 
RUN wget https://github.com/JuliaLang/julia/releases/download/v0.6.1/julia-0.6.1-full.tar.gz && tar -xzf julia-0.6.1-full.tar.gz && rm julia-0.6.1-full.tar.gz
RUN mv julia /opt/julia && cd /opt/julia && make -j 8 JULIA_CPU_TARGET=core2
RUN echo 'export PATH=/root/julia-0.6.1/usr/bin:$PATH' > /etc/profile.d/julia.sh
ENV PATH /opt/conda/bin:/opt/julia/usr/bin:$PATH
RUN apt-get install -y apt-utils vim nano bc
RUN apt-get install -y sudo hdf5-tools
RUN apt-get install -y libssl-dev
#RUN echo 'cd(ENV["HOME"])' >> /opt/julia/usr/etc/julia/juliarc.jl
CMD "/bin/bash" 
