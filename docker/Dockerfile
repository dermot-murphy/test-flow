# ARM Build environment using Segger ARM Compiler

# Base Image
FROM ubuntu:20.04

# Metadata
LABEL MAINTAINER Dermot Murphy <dermot.murphy@canembed.com> Name=arm-environ

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


# Working directory
#WORKDIR /data
#VOLUME ["/data"]

# Entry point (which cannot be overriden on the command line but can be appended to)
#ENTRYPOINT cd /data

# Default command (which can be overridden on the command line)
CMD ["bash"]