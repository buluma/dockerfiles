FROM alpine:3.14

LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

RUN apk upgrade \
    && apk add bash tzdata bind-tools busybox-extras ca-certificates libc6-compat wget curl \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && rm -rf /var/cache/apk/*

CMD ["/bin/bash"]