FROM debian:bullseye-slim
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apt-get update && apt-get install -y \
	ca-certificates \
	gcc \
	git \
	libncurses5 \
	libncurses5-dev \
	libncursesw5 \
	libncursesw5-dev \
	make \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

RUN git clone --depth 1 --recursive https://github.com/visit1985/mdp.git /src

WORKDIR /src

ENV TERM	xterm-256color
ENV DEBUG	1

RUN make \
	&& make install

ENTRYPOINT [ "/usr/local/bin/mdp" ]
