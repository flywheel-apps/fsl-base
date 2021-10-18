FROM neurodebian:xenial
# Xenial is 16
MAINTAINER Flywheel <support@flywheel.io>
ENV DEBIAN_FRONTEND noninteractive


RUN { \
	echo 'deb http://neurodeb.pirsquared.org data main contrib non-free'; \
    echo 'deb http://neurodeb.pirsquared.org xenial main contrib non-free'; \
} > /etc/apt/sources.list.d/neurodebian.sources.list


RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates && \
    rm /usr/share/ca-certificates/mozilla/DST_Root_CA_X3.crt && \
      update-ca-certificates

ENV REQUESTS_CA_BUNDLE "/etc/ssl/certs/ca-certificates.crt"
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:deadsnakes/ppa && \
    apt-get update -y && \
    apt-get install -y python3.7 python3-pip && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN python3.7 -m pip install -U pip && \
    python3.7 -m pip install virtualenv && \
    virtualenv -p /usr/bin/python3.7 venv && \
    . venv/bin/activate && \
    pip install --upgrade pip && \
    apt-get update &&\
    apt-get install -y \
        bc \
        bsdtar \
        curl \
        fsl-5.0-complete \
        jq \
        lsb-core \
        alien=8.95 \
        debhelper=9.20160115ubuntu3 \
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
RUN python -c 'import os, json; f=open("/tmp/gear_environ.json", "w"); json.dump(dict(os.environ), f)'
