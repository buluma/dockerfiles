FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk --no-cache add \
	ncurses

RUN set -x \
	&& apk add --no-cache --virtual .build-deps \
	ca-certificates \
	gcc \
	git \
	libc-dev \
	make \
	&& git clone --depth 1 https://github.com/abs0/wargames.git /tmp/wargames \
	&& ( \
		cd /tmp/wargames \
		&& make \
		&& make install \
	) \
	&& rm -rf /tmp/wargames \
	&& apk del .build-deps

CMD [ "wargames" ]
