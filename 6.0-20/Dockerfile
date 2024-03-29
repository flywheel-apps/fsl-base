FROM ubuntu:focal
MAINTAINER Flywheel <support@flywheel.io>
ENV DEBIAN_FRONTEND noninteractive


# Install dependencies
RUN apt update \
    && apt install -y \
        python2 \
        bc \
        curl \
        jq \
        lsb-core \
        rename \
        wget \
        zip \
        unzip

#############################################
# Download and install FSL 6.0.1
# (see https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FslInstallation/Linux)
# The installation script, fslinstaller.py, needs Python 2.7 to install.
# NOTE: Image almost 10 GB!!!!  This installation of FSL includes all of its
# dependencies... Thus making the docker images almost 10 GB.
# Future Developments may include a "Slimmed" FSL 6.0 docker image
COPY fslinstaller.py /tmp/fslinstaller.py
RUN mkdir -p /usr/share/fsl/
RUN python2 /tmp/fslinstaller.py --fslversion=6.0.4 -d /usr/share/fsl/6.0 -q

# Configure FSL environment
ENV FSLDIR=/usr/share/fsl/6.0
ENV FSL_DIR="${FSLDIR}"
ENV PATH=/usr/share/fsl/6.0/bin/:$PATH
ENV FSLMULTIFILEQUIT=TRUE
ENV POSSUMDIR=/usr/share/fsl/6.0/
ENV LD_LIBRARY_PATH=/usr/share/fsl/6.0/lib:$LD_LIBRARY_PATH
ENV FSLTCLSH=/usr/bin/tclsh
ENV FSLWISH=/usr/bin/wish
ENV FSLOUTPUTTYPE=NIFTI_GZ

# Save docker env to json
RUN python2 -c \
'import os, json; f=open("/tmp/gear_environ.json", "w"); json.dump(dict(os.environ), f)'

#############################################
# Make directory for flywheel spec (v0)
ENV FLYWHEEL=/flywheel/v0
RUN mkdir -p ${FLYWHEEL}