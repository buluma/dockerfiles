# DESCRIPTION:	Create keepass2 container with its dependencies
# AUTHOR:		Christian Koep <christiankoep@gmail.com>
# USAGE:
#	# Build keepass2 image
#	docker build -t keepass2 .
#
#	# Run the container and mount your keepass2 database file
#	docker run -it \
#		-v /home/$USER/DB.kdbx:/root/DB.kdbx \
#		-v /tmp/.X11-unix:/tmp/.X11-unix \
#		-v /home/$USER/keepass2-plugins:/usr/lib/keepass2/Plugins \
#		-e DISPLAY=$DISPLAY \
#		keepass2 "$@"
#
# ISSUES:
#	# 'Gtk: cannot open display: :0'
#	Try to set 'DISPLAY=your_host_ip:0' or run 'xhost +' on your host.
#	(see: https://stackoverflow.com/questions/28392949/running-chromium-inside-docker-gtk-cannot-open-display-0)
#

FROM debian:sid-slim
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV KEEPASSXC_VERSION "release/2.6.1"

RUN buildDeps=' \
		automake \
		argon2-dev \
		asciidoctor \
		bash \
		cmake \
		curl-dev \
		expat \
		g++ \
		gcc \
		git \
		libgcrypt-dev \
		libmicrohttpd-dev \
		libqrencode-dev	\
		libsodium-dev \
		make \
		qt5-qtbase-dev \
		qt5-qtsvg-dev \
		qt5-qttools-dev \
	' \
	set -x \
	&& apk --no-cache add \
		$buildDeps \
	&& git clone --depth 1 --branch ${KEEPASSXC_VERSION} https://github.com/keepassxreboot/keepassxc.git /usr/src/keepassxc \
	&& cd /usr/src/keepassxc \
	&& mkdir build \
	&& cd build \
	&& cmake -DWITH_TESTS=ON -DWITH_XC_AUTOTYPE=ON -DWITH_XC_HTTP=ON .. \
	&& make \
	&& make install \
	&& apk del $buildDeps \
	&& rm -rf /usr/src/keepassxc \
	&& echo "Build complete."

RUN	apk --no-cache add \
		argon2-libs \
		libcurl \
		libmicrohttpd \
		libgcrypt \
		libqrencode \
		libsodium \
		mesa-dri-intel \
		qt5-qtbase \
		qt5-qtbase-x11 \
		qt5-qtsvg \
		qt5-qttools \
		ttf-dejavu

ENTRYPOINT [ "/usr/local/bin/keepassxc" ]
