FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

COPY ./.zshrc /root/.zshrc

RUN apk --no-cache add \
	shadow \
	zsh \
	&& chsh -s /bin/zsh || true

ENV SHELL /usr/bin/zsh

WORKDIR /root
ENTRYPOINT ["/bin/zsh"]
