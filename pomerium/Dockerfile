FROM golang:alpine as builder
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN	apk --no-cache add \
	ca-certificates \
	git \
	make

ENV PATH /go/bin:/usr/local/go/bin:$PATH
ENV GOPATH /go

ENV POMERIUM_VERSION v0.14.7

RUN go get github.com/pomerium/pomerium || true \
	&& cd /go/src/github.com/pomerium/pomerium \
	&& git checkout "${POMERIUM_VERSION}" \
	&& make release \
	&& mv dist/pomerium-linux-amd64 /usr/bin/pomerium


FROM alpine:latest

COPY --from=builder /usr/bin/pomerium /usr/bin/pomerium
COPY --from=builder /etc/ssl/certs/ /etc/ssl/certs

ENTRYPOINT [ "pomerium" ]
