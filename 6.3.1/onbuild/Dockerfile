FROM            alpine:3.4

ENV             NPM_CONFIG_LOGLEVEL=info
ENV             NODE_VERSION=6.3.1

RUN             apk --no-cache add --virtual .build-deps \
                    build-base \
                    curl \
                    linux-headers \
                    binutils \
                    binutils-gold \
                    paxctl \
                    python && \
                mkdir -p /opt/src && \
                curl -sL https://github.com/nodejs/node/archive/v$NODE_VERSION.tar.gz | tar xz -C /opt/src && \
                cd /opt/src/node-$NODE_VERSION && \
                ./configure --prefix=/usr/local && \
                make -j$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
                make install && \
                paxctl -cm /usr/local/bin/node && \
                rm -rf /opt/src && \
                apk --no-cache add --virtual .run-deps \
                    libstdc++ && \
                apk del .build-deps

WORKDIR         /usr/src/app

ONBUILD COPY    package.json /usr/src/app/
ONBUILD RUN     npm install
ONBUILD COPY    . /usr/src/app

CMD             [ "npm", "start" ]
