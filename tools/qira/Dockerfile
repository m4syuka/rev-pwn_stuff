FROM ubuntu:16.04 as base

# prepare packages in env
RUN apt-get update && apt-get -y install libpixman-1-dev curl build-essential debootstrap debian-archive-keyring libjpeg-dev zlib1g-dev unzip wget graphviz curl python-dev python-pip python-virtualenv git wget flex bison libtool automake autoconf autotools-dev pkg-config libglib2.0-dev 
RUN curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py && python2 get-pip.py

# fetch qira
RUN git clone https://github.com/geohot/qira.git
WORKDIR /qira

# install python, build qemu, and link qira
RUN pip install --upgrade -r requirements.txt
RUN cd tracers && ./qemu_build.sh

FROM ubuntu:latest 
COPY --from=base /qira /qira
RUN ln -sf /qira/middleware/qira.py /usr/local/bin/qira
RUN apt-get update && apt-get install wget libc6-i386 gcc make curl -y 
WORKDIR /python
RUN apt-get update && apt-get install build-essential build-essential libc6-dev libexpat1-dev libglib2.0-dev libjpeg-dev libjpeg-turbo8-dev libjpeg8-dev libpcre3-dev libtool zlib1g-dev zlib1g-dev zlib1g zlib1g-dev -y
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install libncursesw5-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev openssl libssl-dev git -y 
RUN git clone https://github.com/yyuu/pyenv.git .pyenv
ENV PYENV_ROOT=/python/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH

RUN echo 'deb http://security.ubuntu.com/ubuntu bionic-security main to' >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32
RUN apt-get update && apt-cache policy libssl1.0-dev &&  apt-get install libssl1.0-dev libevent-dev -y

RUN pyenv install 2.7.10
RUN pyenv global 2.7.10
RUN pyenv rehash
RUN curl -k https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py && python2.7 get-pip.py	
RUN cd /qira && pip install -r requirements.txt

RUN apt-get update && apt-get install graphviz -y 

WORKDIR /tmp
