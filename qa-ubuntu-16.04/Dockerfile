FROM            ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive

## System upgrade
RUN ( \
        apt-get update && \
        apt-get upgrade -y -q && \
        apt-get dist-upgrade -y -q && \
        apt-get -y install locales && \
        apt-get -y -q autoclean && \
        apt-get -y -q autoremove \
    )

## Legato dependencies
RUN ( \
        apt-get update && \
        apt-get --yes --assume-yes install \
                                           build-essential \
                                           python python-jinja2 cmake \
                                           git subversion libsdl-dev \
                                           diffstat texinfo gawk chrpath wget cpio \
                                           vim zsh bash ninja-build screen sshpass \
                                           bc python-git unzip libxml2-utils gcovr \
                                           libcurl4-gnutls-dev zlib1g-dev libbz2-dev \
                                           bsdiff libssl-dev autoconf automake && \
## Optional / Extra
        apt-get --yes --assume-yes install jq openjdk-8-jdk gcovr expect-dev clang && \
## Doc generation
        apt-get --yes --assume-yes install python-bs4 python-xmltodict doxygen graphviz \
                                           linkchecker && \
## QA dependencies
        apt-get --yes --assume-yes install ruby iputils-ping jq netcat sox libxml2-utils python-lxml \
                                           python-pip libglib2.0-dev xsltproc libtool curl \
                                           python-pytest python-pexpect apt-transport-https lsb-release \
                                           ckermit openssh-server && \
## uLegato dependencies (partial)
        apt-get --yes --assume-yes install \
                                           libtool flex gperf bison libncursesw5-dev \
                                           libncurses5-dev && \
## Platform-specific dependencies
        apt-get --yes --assume-yes install \
                                           python-pycparser python-crypto dos2unix p7zip-rar \
                                           lzop libncurses5-dev libncursesw5-dev lcov libc6-dev-i386 && \
## Testbench dependencies
        apt-get --yes --assume-yes install dnsmasq sudo iptables socat openssh-server \
                                           python3-serial && \
## Testbench usage
        apt-get --yes --assume-yes install usbutils pciutils minicom uucp net-tools sshfs && \
        ( curl -sL https://deb.nodesource.com/setup_8.x | bash - ) && \
        ( curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - ) && \
        echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
        apt-get update && \
        apt-get --yes --assume-yes install yarn && \
## LeTP dependencies
        apt-get --yes --assume-yes install telnet && \
## Leaf dependencies
        apt-get --yes --assume-yes install python3 python3-requests python3-argcomplete python3-all python3-setuptools \
                                           python3-pip && \
## Atlas (& qemu) dependencies
        apt-get --yes --assume-yes install vim expect-dev curl build-essential zlib1g-dev libglib2.0-dev libpixman-1-dev git \
                                           libcap-ng-dev libncurses5-dev libcurl4-openssl-dev libusb-dev \
                                           tcsh xsltproc g++ ddd dos2unix mono-runtime gawk gtk+-2.0 \
                                           libpcsclite-dev libpcap-dev uuid-dev apt-file \
                                           libjpeg-progs libjpeg8-dev libjpeg8 libxml2-dev flex bison \
                                           python3.5-dev && \
        apt-get clean \
    )

## Install python dependencies
RUN pip install --upgrade \
                pip \
                openpyxl \
                tap.py \
                six \
                pytest-bdd \
                requests

## UTF8 support
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN ln -sf bash /bin/sh

