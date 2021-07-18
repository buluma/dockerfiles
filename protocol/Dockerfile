FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN buildDeps=' \
               ca-certificates \
               openssl \
       ' \
       && apk --no-cache add --update \
       python3 \
       $buildDeps \
       && wget https://github.com/luismartingarcia/protocol/archive/master.zip \
       && unzip master.zip \
       && cd protocol-master && python3 setup.py install \
       && apk del --purge $buildDeps

ENTRYPOINT ["protocol"]
