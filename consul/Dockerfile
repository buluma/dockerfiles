# busybox wget doesn't support SSL, no curl available :-(
#FROM busybox:latest
# Alpine keeps breaking stuff, even after adding libc6-compat:
# Error relocating ./consul: __fprintf_chk: symbol not foundError relocating ./consul: __fprintf_chk: symbol not found
# rather than downloading glibc with a tonne of extra commands, just switch to debian
#FROM alpine:latest
FROM debian:latest
LABEL maintainer "Michael Buluma <buluma@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

LABEL Description="HashiCorp's Consul minimal" \
      "Consul Version"="$CONSUL_VERSION"

# faster, cached
#COPY consul /

#ADD https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip

RUN bash -c ' \
    set -euxo pipefail && \
    #apk add --no-cache wget unzip ca-certificates && \
    apt-get update && \
    apt-get install -y wget unzip net-tools && \
    wget -t 100 --retry-connrefused -O "consul_${CONSUL_VERSION}_linux_amd64.zip" "https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip" && \
    unzip "consul_${CONSUL_VERSION}_linux_amd64.zip" && \
    rm -fv "consul_${CONSUL_VERSION}_linux_amd64.zip" && \
    chmod +x consul && \
    ls -l && \
    #apk del wget unzip ca-certificates
    apt-get purge -y wget unzip && \
    apt-get autoremove -y && \
    apt-get clean \
    '

#COPY entrypoint.sh /

EXPOSE 8400 8500 8600

#ENTRYPOINT ["/entrypoint.sh"]
ENTRYPOINT ["/consul"]
