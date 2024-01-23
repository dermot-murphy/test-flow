# ARM Build environment using Segger ARM Compiler

# Base Image
FROM ubuntu:20.04

# Metadata
LABEL MAINTAINER Dermot Murphy <dermot.murphy@canembed.com> Name=arm-environ

# Arguments (AStyle)
ARG ASTYLE_VER_MAJOR=3
ARG ASTYLE_VER_MINOR=4
ARG ASTYLE_VER_PATCH=11
ARG ASTYLE_FILENAME=astyle-${ASTYLE_VER_MAJOR}.${ASTYLE_VER_MINOR}.${ASTYLE_VER_PATCH}.tar.bz2
ARG ASTYLE_ROOT=https://downloads.sourceforge.net/project/astyle/astyle/astyle%20${ASTYLE_VER_MAJOR}.${ASTYLE_VER_MINOR}
ARG ASTYLE_URL=${ASTYLE_ROOT}/${ASTYLE_FILENAME}
ARG ASTYLE_TARGET=/astyle

#  This is needed on Ubuntu 20.04 to ensure doxygen and graphviz install without causing Ubuntu to ask for a geographical time zone region
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/London

# Basic development environments
ENV RUNNING=BASIC
RUN	apt-get update && \
        apt-get install -y libx11-6 libfreetype6 libxrender1 libfontconfig1 libxext6 libc6-dev-i386 libc6-dev-i386-amd64-cross
RUN	apt-get install -y zip curl wget unzip			&& \
        apt-get install -y make					&& \
        apt-get install -y git 					&& \
        apt-get install -y subversion

RUN	apt-get install -y doxygen graphviz

RUN	apt-get install -y gcc					&& \
        apt-get install -y cpio libncurses5			&& \
        apt-get install -y ninja-build

# Python 3	
RUN	apt-get install -y python3 python3-pip

# PyTest
RUN     pip install PyTest

# Robot Framework
RUN     pip install Robot

# Gcovr
ENV RUNNING=GCOVR
RUN	pip install gcovr

# CMake (Get the latest release version as Ubuntu has an older version)
# Details at: https://apt.kitware.com/
ENV RUNNING=CMAKE
RUN	apt-get install -y apt-transport-https wget		&&\
        wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | tee /usr/share/keyrings/kitware-archive-keyring.gpg >/dev/null 	 && \
        echo 'deb [signed-by=/usr/share/keyrings/kitware-archive-keyring.gpg] https://apt.kitware.com/ubuntu/ bionic main' | tee /etc/apt/sources.list.d/kitware.list >/dev/null && \
        apt-get update						&& \
        rm /usr/share/keyrings/kitware-archive-keyring.gpg 	&& \
        apt-get install -y kitware-archive-keyring		&& \
        apt-get install -y cmake

# Ceedling
ENV RUNNING=CEEDLING
RUN	apt-get install -y ruby-full				&& \
        gem install rake ceedling

# AStyle
ENV RUNNING=ASTYLE
RUN	mkdir -p ${ASTYLE_TARGET}				&& \
        cd ${ASTYLE_TARGET}					&& \
        wget  ${ASTYLE_URL} -O astyle.tar.gz			&& \
        tar -xvf astyle.tar.gz --strip-components 1		&& \
        cd build						&& \
        cmake .. -GNinja					&& \
        cmake --build .						&& \
        cd ..							&& \
        mkdir bin						&& \
        cp build/astyle bin/astyle				&& \
        rm astyle.tar.gz					&& \
        rm -rf build
ENV PATH="${ASTYLE_TARGET}/bin:${PATH}"

# Working directory
#WORKDIR /data
#VOLUME ["/data"]

# Entry point (which cannot be overriden on the command line but can be appended to)
#ENTRYPOINT cd /data

# Default command (which can be overridden on the command line)
CMD ["bash"]