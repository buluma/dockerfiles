FROM debian:stretch-slim
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

ENV POWERSHELL_VERSION 7.1.3

RUN apt-get update && apt-get install -y \
	ca-certificates \
	dpkg \
	libcurl3 \
	libicu57 \
	libssl1.0.2 \
	liblttng-ust0 \
	libunwind8 \
	wget \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

RUN cd /usr/src \
	&& wget "https://github.com/PowerShell/PowerShell/releases/download/v${POWERSHELL_VERSION}/powershell_${POWERSHELL_VERSION}-1.debian.9_amd64.deb" -O /tmp/powershell.deb \
	&& dpkg -i /tmp/powershell.deb \
	&& ln -snf "/opt/microsoft/powershell/7/pwsh" /usr/bin/pwsh \
	&& apt-get install -fy \
	&& rm -rf /var/lib/apt/lists/* /usr/src/* /tmp/powershell.deb \
	&& which pwsh

ENTRYPOINT [ "/usr/bin/pwsh" ]
