FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk --no-cache add \
	libvirt-client

ENTRYPOINT [ "virsh", "-c", "qemu:///system" ]
