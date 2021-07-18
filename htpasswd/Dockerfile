FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk add --no-cache \
	apache2-utils

ENTRYPOINT [ "htpasswd" ]
