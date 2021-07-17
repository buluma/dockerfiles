# command to run Telnet
# docker run -it --rm \
#	--log-driver none \
#	jess/telnet towel.blinkenlights.nl
#
FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

# RUN apk add --no-cache --virtual \
	busybox-extras
RUN apk add --no-cache busybox-extras

ENTRYPOINT [ "telnet" ]
