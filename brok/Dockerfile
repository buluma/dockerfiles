FROM haskell:8.8

LABEL maintainer "Michael Buluma <buluma@buluma.co.ke>"

ENV TZ 'Afria/Nairobi'

ENV TZ ${TZ}

RUN cabal update && cabal install brok

CMD ["brok"]
