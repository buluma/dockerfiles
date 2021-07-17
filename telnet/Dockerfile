# command to run Telnet
# docker run -it --rm \
#	--log-driver none \
#	jess/telnet towel.blinkenlights.nl
#
FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

# RUN apk add --no-cache --virtual \ https://github.com/jessfraz/dockerfiles/pull/561
# busybox-extras

RUN apk add --no-cache \
	busybox-extras

ENTRYPOINT [ "telnet" ]
