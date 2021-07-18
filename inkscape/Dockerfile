# Run inkscape in a container
#
# docker run -v /tmp/.X11-unix:/tmp/.X11-unix \
#	-v /inkscape/:/workspace \
#	-e DISPLAY=unix$DISPLAY \
#	jess/inkscape
#
FROM ubuntu:16.04
#TODO Upgrade to 20.04
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
	python-software-properties \
	software-properties-common

RUN add-apt-repository ppa:inkscape.dev/stable && \
	apt-get update && apt-get install -y \
	inkscape \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

VOLUME /workspace
WORKDIR /workspace

ENTRYPOINT [ "inkscape" ]
