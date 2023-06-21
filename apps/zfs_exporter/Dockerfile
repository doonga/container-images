FROM ghcr.io/onedr0p/ubuntu:rolling@sha256:bf9d397aeaba6a23dee2a3aff909861cbb02e02deb766f582db5100a11839a32

ARG TARGETPLATFORM
ARG TARGETARCH
ARG TARGETOS

ARG VERSION

LABEL dev.doonga.image.target_platform=$TARGETPLATFORM
LABEL dev.doonga.image.target_architecture=$TARGETARCH
LABEL dev.doonga.image.target_os=$TARGETOS
LABEL org.opencontainers.image.source="https://github.com/pdf/zfs_exporter/"

ENV PATH="${PATH}:/sbin"

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
        | tar -xz --strip-components=2 -C /temp/ \
    cp /temp/zfs_exporter /bin/

USER nobody

EXPOSE 9134
ENTRYPOINT  [ "/bin/zfs_exporter" ]
