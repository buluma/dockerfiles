FROM alpine:3.13

LABEL maintainer="buluma <ops@buluma.me.ke>"

ARG TZ="Africa/Nairobi"

ENV TZ ${TZ}
ENV CRYPTOGRAPHY_DONT_BUILD_RUST=1

COPY Gemfile Gemfile

RUN apk upgrade --update \
    && apk add bash build-base libffi zlib libxml2 \
        libxslt ruby ruby-io-console ruby-json yaml openssl-dev \
        nodejs git perl tzdata \
    && apk add --virtual .build-deps \
        build-base libffi-dev zlib-dev libxml2-dev \
        libxslt-dev ruby-dev \
    && echo 'gem: --no-document' >> ~/.gemrc \
    && cp ~/.gemrc /etc/gemrc \
    && chmod uog+r /etc/gemrc \
    && gem install bundler \
    && gem install open-uri \
    && gem install --system \
    && bundle config build.jekyll --no-rdoc \
    && bundle install \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && apk del .build-deps \
    && rm -rf /Gemfile* \
            /var/cache/apk/* \
            /usr/lib/lib/ruby/gems/*/cache/* \
            ~/.gem

WORKDIR /root

CMD ["/bin/bash"]