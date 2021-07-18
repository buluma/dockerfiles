# ab (apache benchmark)
# in a container
#
# docker run --rm -it \
# 	buluma/ab
#
FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

RUN apk --no-cache add \
	apache2-ssl \
	apache2-utils \
	ca-certificates \
	htop

ENTRYPOINT [ "ab" ]
