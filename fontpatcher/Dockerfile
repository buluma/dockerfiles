FROM debian:sid-slim
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apt-get update && apt-get install -y \
	python-fontforge \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

RUN buildDeps=' \
		ca-certificates \
		git \
	' \
	set -x \
	&& apt-get update \
	&& apt-get install -y $buildDeps --no-install-recommends \
	&& git clone --depth 1 --branch develop https://github.com/Lokaltog/vim-powerline.git /pwrline \
	&& ( \
		cd /pwrline \
		&& mv fontpatcher/fontpatcher /usr/bin/ \
		&& mv fontpatcher/PowerlineSymbols.sfd /usr/bin/ \
	) \
	&& rm -rf /pwrline \
	&& apt-get purge -y --auto-remove $buildDeps \
	&& rm -rf /var/lib/apt/lists/* \
	&& echo "Build complete."

ENTRYPOINT [ "fontpatcher" ]
