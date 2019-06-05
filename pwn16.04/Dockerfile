FROM ubuntu:18.04

RUN dpkg --add-architecture i386 \
    && apt-get update \
    && apt-get install libstdc++6:i386 libgcc1:i386 zlib1g:i386 libncurses5:i386 -y

RUN apt-get install gdb python2.7 python-pip python-dev git libssl-dev libffi-dev build-essential -y \
    && python -m pip install --upgrade pip \
    && python -m pip install --upgrade pwntools

RUN git clone https://github.com/pwndbg/pwndbg \
    && cd pwndbg \
    && ./setup.sh
