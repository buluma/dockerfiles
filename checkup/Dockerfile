FROM golang:alpine as builder
LABEL maintainer "Michael Buluma <buluma@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN	apk --no-cache add \
	ca-certificates \
	gcc \
	git \
	libc-dev

ENV PATH /go/bin:/usr/local/go/bin:$PATH
ENV GOPATH /go

RUN go get github.com/sourcegraph/checkup/cmd/checkup

FROM alpine:latest

COPY --from=builder /go/bin/checkup /usr/bin/checkup
COPY --from=builder /etc/ssl/certs/ /etc/ssl/certs

ENTRYPOINT [ "checkup" ]
