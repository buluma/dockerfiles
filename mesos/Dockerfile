FROM harisekhon/debian-java:jre7
# FROM buluma/debian-java:jre7
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

ARG MESOS_VERSION=0.28.2

#ARG TAR="mesos-$MESOS_VERSION.tar.gz"

ENV PATH $PATH:/mesos/bin

LABEL Description="Apache Mesos" \
      "Apache Mesos Version"="$MESOS_VERSION"

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /

# debian uses sh -c by default which doesn't recognize the ${var:n:n}
RUN bash -c '\
    set -euxo pipefail && \
    apt-get update && \
    # need net-tools for ifconfig in /entrypoint.sh
    apt-get install -y --no-install-recommends wget net-tools && \
    # Apache only ships source, don't want entire dev tooling in image
    #apt-get install -y --no-install-recommends tar wget && \
    #wget -t 10 --retry-connrefused "http://archive.apache.org/dist/mesos/$MESOS_VERSION/$TAR" && \
    #tar zxvf "$TAR" && \
    #rm -v "$TAR" && \
    #ln -sf "mesos-$MESOS_VERSION" mesos && \
    #
    # doesn't take past release version suffixes and repo is non-browseable (MESOS-5608)
#    apt-get install -y --no-install-recommends lsb-release && \
#    apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF && \
#    DISTRO=$(lsb_release -is | tr '[:upper:]' '[:lower:]') && \
#    CODENAME=$(lsb_release -cs) && \
#    echo "deb http://repos.mesosphere.io/${DISTRO} ${CODENAME} main" | tee /etc/apt/sources.list.d/mesosphere.list && \
#    apt-get update && \
#
    if   [ "${MESOS_VERSION:0:4}" = "0.23" ]; then file="mesos_$MESOS_VERSION-1.0.debian81_amd64.deb"; \
    elif [ "${MESOS_VERSION:0:4}" = "0.24" ]; then file="mesos_$MESOS_VERSION-2.0.17.debian81_amd64.deb"; \
    elif [ "${MESOS_VERSION:0:4}" = "0.25" ]; then file="mesos_$MESOS_VERSION-2.0.21.debian81_amd64.deb"; \
    elif [ "${MESOS_VERSION:0:4}" = "0.26" ]; then file="mesos_$MESOS_VERSION-2.0.19.debian81_amd64.deb"; \
    elif [ "${MESOS_VERSION:0:4}" = "0.27" ]; then file="mesos_$MESOS_VERSION-2.0.15.debian81_amd64.deb"; \
    elif [ "${MESOS_VERSION:0:4}" = "0.28" ]; then file="mesos_$MESOS_VERSION-2.0.27.debian81_amd64.deb"; \
    else echo "unexpected mesos version"; exit 1; fi && \
    wget -t 10 --retry-connrefused "http://repos.mesosphere.com/debian/pool/main/m/mesos/$file" && \
    #apt-get install ./mesos*.deb && \
    dpkg -i mesos*.deb || :; \
    apt-get install -yf && \
    dpkg -i mesos*.deb && \
    # attempting to remove tar causes unmet dependency breakage
    apt-get purge -y wget && \
    apt-get autoremove -y && \
    apt-get clean'
COPY entrypoint.sh /
EXPOSE 5050 5051
ENTRYPOINT ["/entrypoint.sh"]
