FROM ghcr.io/onedr0p/ubuntu:rolling@sha256:3d189191fea043275c83d33d4a3c59c2d44fce08cdb48e360310f8f29cef62fe

ARG TARGETPLATFORM
ARG TARGETARCH
ARG TARGETOS

ARG VERSION

LABEL dev.doonga.image.target_platform=$TARGETPLATFORM
LABEL dev.doonga.image.target_architecture=$TARGETARCH
LABEL dev.doonga.image.target_os=$TARGETOS
LABEL org.opencontainers.image.source="https://github.com/pdf/zfs_exporter/"

ENV PATH="${PATH}:/sbin"
ENV DEBIAN_FRONTEND=noninteractive

USER root

#hadolint ignore=DL3018,DL3013
RUN \
    case "${TARGETPLATFORM}" in \
        'linux/amd64') export ARCH='amd64' ;; \
        'linux/arm64') export ARCH='arm64' ;; \
    esac \
    && \
    curl -L \
        "https://github.com/pdf/zfs_exporter/releases/download/v${VERSION}/zfs_exporter-${VERSION}.linux-amd64.tar.gz" \
        | tar -xz --strip-components=1 -C /app/

RUN apt update && apt install -y zfsutils-linux && rm -rf /var/lib/apt/lists/*

USER nobody

EXPOSE 9134
COPY ./entrypoint.sh /entrypoint.sh
CMD ["/entrypoint.sh"]
