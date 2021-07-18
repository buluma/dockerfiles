FROM golang:alpine as builder
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN	apk --no-cache add \
	ca-certificates \
	git

ENV PATH /go/bin:/usr/local/go/bin:$PATH
ENV GOPATH /go

ENV OAUTH2_PROXY_VERSION v7.1.3

RUN go get github.com/pusher/oauth2_proxy || true \
	&& cd /go/src/github.com/pusher/oauth2_proxy \
	&& git checkout "${OAUTH2_PROXY_VERSION}" \
	&& go build . \
	&& mv oauth2_proxy /usr/bin/


FROM alpine:latest

COPY --from=builder /usr/bin/oauth2_proxy /usr/bin/oauth2_proxy
COPY --from=builder /etc/ssl/certs/ /etc/ssl/certs

ENTRYPOINT [ "oauth2_proxy" ]
