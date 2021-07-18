# Run imagemin in a container:
#
# docker run --rm -it \
#	-v /etc/localtime:/etc/localtime:ro \
#	-v $HOME/Pictures:/root/Pictures \
#	--entrypoint bash \
#	jess/imagemin
#
FROM node:alpine
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk --no-cache add \
	file \
	libpng

RUN set -x \
	&& apk add --no-cache --virtual .build-deps \
		autoconf \
		automake \
		build-base \
		libpng-dev \
		nasm \
	&& npm install --global imagemin-cli \
	&& apk del .build-deps

CMD [ "imagemin", "--help" ]
