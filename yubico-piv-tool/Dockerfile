# Run yubico-piv-tool in a container
#
# docker run --rm -it \
# 	--device /dev/bus/usb \
# 	--device /dev/usb
#	--name yubico-piv-tool \
#	jess/yubico-piv-tool
#
FROM ubuntu:16.04
#TODO upgrade to ubuntu20.04
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apt-get update && apt-get install -y \
	software-properties-common \
	--no-install-recommends && \
	add-apt-repository ppa:yubico/stable && \
	apt-get update && apt-get install -y \
	pcscd \
	procps \
	usbutils \
	yubico-piv-tool \
	&& rm -rf /var/lib/apt/lists/*

WORKDIR /root/

COPY entrypoint.sh /usr/local/bin/

ENTRYPOINT [ "/usr/local/bin/entrypoint.sh" ]
CMD [ "yubico-piv-tool", "--help" ]
