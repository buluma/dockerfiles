FROM r.j3ss.co/wireguard:install
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apt update && apt -y install \
	bash \
	bc \
	bison \
	ca-certificates \
	curl \
	fakeroot \
	flex \
	git \
	libgmp-dev \
	libncurses-dev \
	perl \
	tar \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV HOME /root
WORKDIR $HOME

ENV JOBS 4

COPY build_kernel /usr/local/bin/build_kernel

RUN echo "build_kernel [version]" > /root/.bash_history

ENTRYPOINT [ "bash" ]
