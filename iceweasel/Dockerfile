FROM debian:bullseye-slim
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apt-get update && apt-get install -y \
	hicolor-icon-theme \
	firefox-esr \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

COPY local.conf /etc/fonts/local.conf

ENTRYPOINT [ "firefox" ]
