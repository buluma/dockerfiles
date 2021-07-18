FROM alpine:latest
LABEL maintainer "Michael Buluma <buluma@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk --no-cache add \
	ca-certificates \
	python \
	py-boto \
	py-future \
	py-paramiko

RUN buildDeps=' \
		build-base \
		git \
		python-dev \
	' \
	set -x \
	&& apk --no-cache add $buildDeps \
	&& git clone --depth 1 https://github.com/newsapps/beeswithmachineguns /usr/src/beeswithmachineguns \
	&& cd /usr/src/beeswithmachineguns \
	&& python setup.py install \
	&& rm -rf /usr/src/beeswithmachineguns \
	&& apk del $buildDeps

ENTRYPOINT [ "bees" ]
