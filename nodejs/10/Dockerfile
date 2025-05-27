FROM --platform=$TARGETOS/$TARGETARCH arm64v8/node:10-alpine

LABEL author="Michael Parker" maintainer="parker@pterodactyl.io"

# add container user and set stop signal
RUN         useradd -m -d /home/container container
STOPSIGNAL  SIGINT

RUN apt update \
    && apt -y install \
        ffmpeg \
        iproute2 \
        git \
        sqlite3 \
        libsqlite3-dev \
        python3 \
        python3-dev \
        ca-certificates \
        dnsutils \
        tzdata \
        zip \
        tar \
        curl \
        build-essential \
        libtool \
        iputils-ping \
        libnss3 \
        tini

# Nota: Node 10 incluye npm por defecto, no es necesario actualizar npm ni instalar TypeScript si no lo usas.
# Si necesitas alguna versión de npm o typescript compatible, puedes instalar aquí.

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

COPY --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/usr/bin/tini", "-g", "--"]
CMD ["/entrypoint.sh"]
