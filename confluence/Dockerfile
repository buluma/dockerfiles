FROM atlassian/confluence-server:7.4.1

LABEL maintainer="buluma <ops@buluma.me.ke>"

ARG TZ="Africa/Nairobi"

ENV TZ ${TZ}
ENV AGENT_PATH /opt/atlassian-agent.jar

RUN pwd && ls -a confluence/

COPY confluence/atlassian-agent.jar ${AGENT_PATH}
COPY hijack.sh /hijack.sh

RUN set -x \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt update \
    && apt upgrade -y \
    && apt install tzdata -y \
    && chown ${RUN_USER}:${RUN_GROUP} ${AGENT_PATH} \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && dpkg-reconfigure --frontend noninteractive tzdata \
    && apt autoremove -y \
    && apt autoclean -y

CMD ["/hijack.sh"]

