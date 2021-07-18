FROM alpine:latest
LABEL maintainer "Michael Buluma <ops@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN apk --no-cache add \
	imagemagick

CMD [ "echo", "Use one of the following commands [ animate | compare | composite | conjure | convert | display | identify | import | mogrify | montage | stream ]" ]
