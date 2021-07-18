FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

COPY nnp /usr/local/bin/nnp
RUN chmod +s /usr/local/bin/nnp

CMD ["/usr/local/bin/nnp"]
