FROM debian:sid-slim
LABEL maintainer "Michael Buluma <buluma@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apt-get update && apt-get install -y \
	apt-file \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

CMD [ "bash" ]
