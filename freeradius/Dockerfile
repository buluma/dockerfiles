FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk --no-cache add \
    freeradius \
	freeradius-python \
	freeradius-radclient \
	freeradius-sql \
	freeradius-sqlite \
	openssl-dev \
	python2 \
	sqlite

ENTRYPOINT [ "radiusd" ]
CMD [ "-xx","-f" ]
