FROM ubuntu:20.04
LABEL maintainer "buluma <ops@buluma.me.ke>"

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
	byobu \
	hollywood \
	locate \
	mlocate \
	&& rm -rf /var/lib/apt/lists/* \
	&& updatedb

ENV HOME /home/user
RUN useradd --create-home --home-dir $HOME user \
	&& chown -R user:user $HOME

WORKDIR $HOME
USER user

CMD [ "hollywood" ]
