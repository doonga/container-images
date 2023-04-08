FROM ghcr.io/onedr0p/alpine:rolling@sha256:e6a2407a15b7e557fb6617a592f672b004b6764887438502c047a567ec616e40

ARG TARGETPLATFORM
ARG TARGETARCH
ARG TARGETOS

ARG VERSION

LABEL dev.greyrock.image.target_platform=$TARGETPLATFORM
LABEL dev.greyrock.image.target_architecture=$TARGETARCH
LABEL dev.greyrock.image.target_os=$TARGETOS
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
        | tar -xz --strip-components=1 -C /app/ \
    && mkdir -p /config \
    && chown -R root:root /app \
    && chmod -R 755 /app \
    && chown -R kah:kah /config

USER kah
COPY ./apps/ctrld/entrypoint.sh /entrypoint.sh
CMD ["/entrypoint.sh"]
