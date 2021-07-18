FROM alpine:latest

LABEL maintainer "Michael Buluma <buluma@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk --no-cache add \
	ca-certificates \
	python \
	py2-pip \
	&& pip install cli53

ENTRYPOINT [ "cli53" ]
