FROM python:3-alpine
LABEL maintainer "Michael Buluma <buluma@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk add --no-cache \
	bash

RUN set -x \
	&& apk add --no-cache --virtual .build-deps \
		build-base \
		libffi-dev \
		openssl-dev \
	&& pip install --upgrade \
		--pre azure-cli \
		--extra-index-url https://azurecliprod.blob.core.windows.net/edge \
		--no-cache-dir \
	&& apk del .build-deps

ENTRYPOINT	[ "az" ]
