FROM r.j3ss.co/curl
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk add --no-cache \
	bash

COPY sendemail /usr/bin/sendemail

ENTRYPOINT [ "sendemail" ]
