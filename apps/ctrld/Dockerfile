FROM ghcr.io/onedr0p/ubuntu:rolling@sha256:5924c65dfc7db291ae97cb409812ea6b828357daeef6b34ef72eb434cc0438e3

ARG TARGETPLATFORM
ARG TARGETARCH
ARG TARGETOS

ARG VERSION

LABEL dev.doonga.image.target_platform=$TARGETPLATFORM
LABEL dev.doonga.image.target_architecture=$TARGETARCH
LABEL dev.doonga.image.target_os=$TARGETOS
LABEL org.opencontainers.image.source="https://github.com/Control-D-Inc/ctrld"

ENV CTRLD_CONFIG_FILE "/config/ctrld.toml"

#hadolint ignore=DL3018,DL3013
RUN \
    case "${TARGETPLATFORM}" in \
        'linux/amd64') export ARCH='amd64' ;; \
        'linux/arm64') export ARCH='arm64' ;; \
    esac \
    && \
    curl -L \
        "https://github.com/Control-D-Inc/ctrld/releases/download/v${VERSION}/ctrld_${VERSION}_linux_${ARCH}.tar.gz" \
        | tar -xz --strip-components=2 -C /app/ \
    && mkdir -p /etc/controld \
    && mkdir -p /config \
    && chown -R root:root /app \
    && chmod -R 755 /app \
    && chown -R kah:kah /config

USER kah
COPY ./apps/ctrld/entrypoint.sh /entrypoint.sh
CMD ["/entrypoint.sh"]
