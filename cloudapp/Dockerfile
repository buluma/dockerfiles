FROM	ruby:alpine
LABEL maintainer "Michael Buluma <buluma@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN	apk add --no-cache \
	libcurl

RUN	set -x \
	&& apk add --no-cache --virtual .build-deps \
	build-base \
	&& gem install cloudapp --no-document \
	&& apk del .build-deps

ENTRYPOINT	["cloudapp"]
