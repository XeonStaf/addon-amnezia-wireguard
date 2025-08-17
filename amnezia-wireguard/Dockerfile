ARG BUILD_FROM=ghcr.io/hassio-addons/base:17.2.1
FROM ${BUILD_FROM}

# Amnezia Wireguard Tools version
ENV AWG_TOOLS=v1.0.20241018
# AmneziaWG-Go version
ENV AWG_GO=v0.2.12

# Используем bash с pipefail
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# На всякий случай добавим /usr/bin в PATH
ENV PATH="/usr/bin:/sbin:/usr/sbin:${PATH}"

# Build-зависимости
RUN apk add --no-cache --virtual .build-dependencies \
      build-base \
      linux-headers \
      git

# Runtime-зависимости
RUN apk add --no-cache \
      go \
      iptables \
      libqrencode-tools \
      openresolv \
      iproute2 \
  && { [ -x /sbin/ip ] && ln -sf /sbin/ip /usr/bin/ip || true; } \
  && { [ -x /usr/sbin/ip ] && ln -sf /usr/sbin/ip /usr/bin/ip || true; } \
  && ln -sf /sbin/xtables-nft-multi /sbin/ip6tables \
  && ln -sf /sbin/xtables-nft-multi /sbin/iptables

# Сборка awg-tools
RUN git clone --depth=1 --branch $AWG_TOOLS \
      "https://github.com/amnezia-vpn/amneziawg-tools.git" /tmp/wg-tools \
  && cd /tmp/wg-tools/src && make && make install

# Сборка amneziawg-go
RUN git clone --depth=1 --branch $AWG_GO \
      "https://github.com/amnezia-vpn/amneziawg-go.git" /tmp/wireguard \
  && cd /tmp/wireguard && make && make install \
  && rm -rf /tmp/* \
  && apk del --no-cache --purge .build-dependencies go

# Копируем rootfs аддона
COPY rootfs /

# Build args
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="fork Franck Nijhof <frenck@addons.community>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Franck Nijhof <frenck@addons.community>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
ARG BUILD_FROM=ghcr.io/hassio-addons/base:17.2.1
FROM ${BUILD_FROM}

# Amnezia Wireguard Tools version
ENV AWG_TOOLS=v1.0.20241018
# AmneziaWG-Go version
ENV AWG_GO=v0.2.12

# Используем bash с pipefail
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# На всякий случай добавим /usr/bin в PATH
ENV PATH="/usr/bin:/sbin:/usr/sbin:${PATH}"

# Build-зависимости
RUN apk add --no-cache --virtual .build-dependencies \
      build-base \
      linux-headers \
      git

# Runtime-зависимости
RUN apk add --no-cache \
      go \
      iptables \
      libqrencode-tools \
      openresolv \
      iproute2 \
  && { [ -x /sbin/ip ] && ln -sf /sbin/ip /usr/bin/ip || true; } \
  && { [ -x /usr/sbin/ip ] && ln -sf /usr/sbin/ip /usr/bin/ip || true; } \
  && ln -sf /sbin/xtables-nft-multi /sbin/ip6tables \
  && ln -sf /sbin/xtables-nft-multi /sbin/iptables

# Сборка awg-tools
RUN git clone --depth=1 --branch $AWG_TOOLS \
      "https://github.com/amnezia-vpn/amneziawg-tools.git" /tmp/wg-tools \
  && cd /tmp/wg-tools/src && make && make install

# Сборка amneziawg-go
RUN git clone --depth=1 --branch $AWG_GO \
      "https://github.com/amnezia-vpn/amneziawg-go.git" /tmp/wireguard \
  && cd /tmp/wireguard && make && make install \
  && rm -rf /tmp/* \
  && apk del --no-cache --purge .build-dependencies go

# Копируем rootfs аддона
COPY rootfs /

# Build args
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="fork Franck Nijhof <frenck@addons.community>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Franck Nijhof <frenck@addons.community>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
