# Base image
FROM kalilinux/kali-linux-docker

# Minimal package installation
# ruamel will get installed by setup.py via pip, but this just makes the
# process smoother. If it were to be installed by PyBOMBS itselfs, this would
# be a different story and we'd not include it here.
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
	apt-utils \
	python-apt \
	python-pip \
	python-ruamel.yaml

WORKDIR /pybombs
COPY . /pybombs/
RUN python setup.py -q install

WORKDIR /prefix
RUN pybombs auto-config && pybombs recipes add-defaults
RUN pybombs prefix init -a default -R gnuradio-default default
RUN pybombs install gr-gsm
