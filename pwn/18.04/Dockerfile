FROM ubuntu:18.04
ENV LIBC_TAG=glibc-2.27

RUN dpkg --add-architecture i386 \
    && apt-get update \
    && apt-get install libstdc++6:i386 libgcc1:i386 zlib1g:i386 libncurses5:i386 -y

RUN apt-get install gdb python2.7 python-pip python-dev git libssl-dev libffi-dev build-essential -y \
    && python -m pip install --upgrade pip \
    && python -m pip install --upgrade pwntools

RUN git clone https://github.com/pwndbg/pwndbg \
    && cd pwndbg \
    && ./setup.sh

# debug version of libc

RUN git clone --depth=1 --branch $LIBC_TAG https://github.com/bminor/glibc.git

RUN apt-get install gawk gcc-multilib g++-multilib bison -y

# 64bit version

RUN mkdir /libc-build \
    && mkdir /libc-dbg

RUN cd /libc-build \
    && /glibc/configure --prefix=$HOME/glibc32 \
    && make -j $(nproc) \
    && cp /libc-build/libc.so /libc-dbg/libc64.so \
    && rm -rf *

# 32bit version

RUN cd /libc-build \
    && /glibc/configure --prefix=$HOME/glibc32 \
     --host=i686-linux-gnu \
     --build=i686-linux-gnu \
     CC="gcc -m32" CXX="g++ -m32" \
     CFLAGS="-O2 -march=i686" \
     CXXFLAGS="-O2 -march=i686" \
    && make -j $(nproc) \
    && cp /libc-build/libc.so /libc-dbg/libc32.so \
    && rm -rf *

RUN rm -rf /var/lib/apt/lists/*
