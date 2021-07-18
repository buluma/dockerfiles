FROM golang:alpine as builder
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk --no-cache add \
	ca-certificates \
	git \
	make

ENV PATH /go/bin:/usr/local/go/bin:$PATH
ENV GOPATH /go

ENV MICRO_VERSION v2.0.9

RUN git clone --depth 1 --branch "$MICRO_VERSION" https://github.com/zyedidia/micro /go/src/github.com/zyedidia/micro

WORKDIR /go/src/github.com/zyedidia/micro

RUN make install

FROM alpine:latest

COPY --from=builder /go/bin/micro /usr/bin/micro
COPY --from=builder /etc/ssl/certs/ /etc/ssl/certs

ENTRYPOINT [ "micro" ]
