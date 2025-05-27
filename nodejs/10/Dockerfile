FROM --platform=$TARGETOS/$TARGETARCH arm64v8/node:10-alpine

LABEL author="RADD95" maintainer="radd95@example.com"

# Instalar el paquete shadow para poder usar useradd
RUN apk add --no-cache shadow

# Agregar el usuario container y configurar la señal de detención
RUN useradd -m -d /home/container container
STOPSIGNAL SIGINT

# Instalar dependencias necesarias
RUN apk update && apk add --no-cache \
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
    build-base \
    libtool \
    iputils \
    libnss3 \
    tini

# Nota: Node 10 incluye npm por defecto, no es necesario actualizar npm ni instalar TypeScript si no lo usas.

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

# Copiar el script entrypoint.sh
COPY --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# Establecer el entrypoint
ENTRYPOINT ["/usr/bin/tini", "-g", "--"]
CMD ["/entrypoint.sh"]
