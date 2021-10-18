FROM ubuntu:focal
MAINTAINER Flywheel <support@flywheel.io>
ENV DEBIAN_FRONTEND noninteractive
ENV NEURODEB_KEY http://neuro.debian.net/_static/neuro.debian.net.asc


# Install dependencies


RUN apt-get update && \
    apt-get install -y gnupg && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys A5D32F012649A5A9

RUN echo deb http://neuro.debian.net/debian data main contrib non-free >> /etc/apt/sources.list.d/neurodebian.sources.list && \
    echo deb http://neuro.debian.net/debian focal main contrib non-free >> /etc/apt/sources.list.d/neurodebian.sources.list

RUN apt-get update && \
    apt-get install -y \
        bc \
        libarchive-tools \
        fsl-5.0 \
        jq \
        lsb-core \
        python3 \
        python3-pip \
        rename \
        zip

# Make directory for flywheel spec (v0)
ENV FLYWHEEL=/flywheel/v0
RUN mkdir -p ${FLYWHEEL}

# Set ENV variables
ENV FSLBROWSER=/etc/alternatives/x-www-browser
ENV FSLDIR=/usr/share/fsl/5.0
ENV FSLMULTIFILEQUIT=TRUE
ENV FSLOUTPUTTYPE=NIFTI_GZ
ENV FSLTCLSH=/usr/bin/tclsh
ENV FSLWISH=/usr/bin/wish
ENV LD_LIBRARY_PATH=/usr/lib/fsl/5.0
ENV PATH=/usr/lib/fsl/5.0:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV POSSUMDIR=/usr/share/fsl/5.0

# Save docker env to json
RUN python3 -c 'import os, json; f=open("/tmp/gear_environ.json", "w"); json.dump(dict(os.environ), f)'
