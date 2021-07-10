# #
# #  Author: Hari Sekhon
# #  Date: 2016-01-16 09:58:07 +0000 (Sat, 16 Jan 2016)
# #
# #  vim:ts=4:sts=4:sw=4:et
# #
# #  https://github.com/harisekhon/Dockerfiles
# #
# #  If you're using my code you're welcome to connect with me on LinkedIn and optionally send me feedback to help improve or steer this or other code I publish
# #
# #  https://www.linkedin.com/in/harisekhon
# #

# # -dev version allows testing of local consul command utils like check_consul_version.py

# # busybox wget doesn't support SSL, no curl available :-(
# #FROM busybox:latest
# # Alpine keeps breaking stuff, even after adding libc6-compat:
# # Error relocating ./consul: __fprintf_chk: symbol not foundError relocating ./consul: __fprintf_chk: symbol not found
# # rather than downloading glibc with a tonne of extra commands, just switch to debian
# #FROM harisekhon/alpine-github:latest
# # FROM harisekhon/centos-github:latest
# FROM buluma/consul-dev:latest
# MAINTAINER Michael Buluma

# ARG CONSUL_VERSION=1.9.7

# ENV PATH $PATH:/

# LABEL Description="HashiCorp's Consul + Dev tools" \
#       "Consul Version"="$CONSUL_VERSION"

# WORKDIR /

# # faster, cached
# # COPY consul-dev /

# #ADD https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip

# RUN set -eux && \
#     yum install -y wget unzip net-tools && \
#     wget -t 100 --retry-connrefused -O "consul_${CONSUL_VERSION}_linux_amd64.zip" "https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip" && \
#     unzip -o "consul_${CONSUL_VERSION}_linux_amd64.zip" && \
#     rm -fv "consul_${CONSUL_VERSION}_linux_amd64.zip" && \
#     yum remove -y wget unzip && \
#     yum autoremove -y && \
#     yum clean all && \
#     rm -rf /var/cache/yum

# #COPY entrypoint.sh /

# EXPOSE 8400 8500 8600

# CMD ["/consul", "agent", "-dev", "-data-dir", "/tmp", "-client", "0.0.0.0"]

FROM golang:latest as builder
MAINTAINER Michael Buluma

ENV PATH /go/bin:/usr/local/go/bin:$PATH
ENV GOPATH /go

RUN apt-get update && apt-get install -y \
	apt-transport-https \
	ca-certificates \
	curl \
	gcc \
	git \
	make \
	ruby-dev \
	ruby \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

# Add yarn to apt repos.
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Setup node install.
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -

RUN apt-get update && apt-get install -y \
	nodejs \
	yarn \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV CONSUL_VERSION v1.8.0-beta2

RUN go get github.com/hashicorp/consul || true

WORKDIR /go/src/github.com/hashicorp/consul

RUN git checkout "${CONSUL_VERSION}"

# Install deps for UI.
RUN gem install \
	bundler \
	--no-ri --no-rdoc

RUN cd ui-v2 \
	&& yarn install \
	&& make \
	&& rm -rf ../pkg/web_ui \
	&& mkdir -p ../pkg \
	&& cp -r dist ../pkg/web_ui

RUN TERM=xterm XC_ARCH="amd64" XC_OS="linux" LD_FLAGS=" -extldflags -static" make tools static-assets bin \
	&& mv bin/consul /usr/bin/consul

FROM alpine:latest

COPY --from=builder /usr/bin/consul /usr/bin/consul
COPY --from=builder /etc/ssl/certs/ /etc/ssl/certs

ENTRYPOINT [ "consul" ]
CMD [ "--help" ]

