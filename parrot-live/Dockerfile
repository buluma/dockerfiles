FROM node:alpine
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk add --no-cache git
RUN git clone --branch master --depth 1 https://github.com/hugomd/parrot.live.git /src
WORKDIR /src
RUN npm install
CMD ["node","index.js"]
