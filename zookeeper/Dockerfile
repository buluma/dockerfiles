FROM alpine:latest
MAINTAINER Michael Buluma

ARG ZOOKEEPER_VERSION=3.6.3
ARG TAR=apache-zookeeper-${ZOOKEEPER_VERSION}.tar.gz

ENV PATH $PATH:/zookeeper/bin

LABEL Description="ZooKeeper" \
      "ZooKeeper Version"="$ZOOKEEPER_VERSION"

WORKDIR /

# bash => entrypoint.sh
# java => zookeeper
RUN set -eux && \
    apk add --no-cache bash openjdk8-jre-base

RUN set -eux && \
    apk add --no-cache wget tar && \
    # url="http://www.apache.org/dyn/closer.lua?filename=zookeeper/zookeeper-${ZOOKEEPER_VERSION}/${TAR}&action=download" && \
    url="https://downloads.apache.org/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/${TAR}" && \
    url_archive="http://archive.apache.org/dist/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/${TAR}" && \
    wget -t 5 --retry-connrefused -O "$TAR" "$url" || \
    wget -t 5 --retry-connrefused -O "$TAR" "$url_archive" && \
    pwd && \
    tar zxf "${TAR}" && \
    rm -fv "${TAR}" && \
    ls -a . && \
    ln -sv /apache-zookeeper-${ZOOKEEPER_VERSION} /zookeeper && \
    cp -av zookeeper/conf/zoo_sample.cfg /zookeeper/conf/zoo.cfg && \
    # rm -rf zookeeper/src zookeeper/docs && \
    # apk del wget tar

EXPOSE 2181 3181 4181

COPY entrypoint.sh /

CMD ["/entrypoint.sh"]
