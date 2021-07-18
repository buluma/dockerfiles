FROM debian:sid-slim
LABEL maintainer "Michael Buluma <buluma@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apt-get update && apt-get install -y \
	ca-certificates \
	curl \
	distcc \
	git \
	make \
	libncurses5-dev \
	libssl-dev \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV HOME /root
WORKDIR $HOME

COPY distccd-init /usr/local/bin/distccd-init

ENTRYPOINT [ "distccd-init" ]
