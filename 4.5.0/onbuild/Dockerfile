FROM            allanlei/node:4.5.0

WORKDIR         /usr/src/app

ONBUILD COPY    package.json /usr/src/app/
ONBUILD RUN     apk --no-cache add --virtual .build-deps \
                    build-base \
                    python && \
                npm install && \
                apk --no-cache del .build-deps
ONBUILD COPY    . /usr/src/app

CMD             [ "npm", "start" ]
