FROM	ruby:alpine
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN	apk add --no-cache \
	ca-certificates \
	git

RUN	set -x \
	&& apk add --no-cache --virtual .build-deps \
	build-base \
	&& gem install travis --no-document \
	&& apk del .build-deps

ENTRYPOINT	["travis"]
