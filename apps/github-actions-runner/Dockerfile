ARG VERSION=latest@sha256:18bf08879ba083b5469008fa9157d5bfec5496150ed81ead407cd71b7eb928ae

FROM ghcr.io/actions/actions-runner:${VERSION}

# hadolint ignore=DL3008,DL3015,SC2086
RUN \
    sudo apt-get -qq update \
    && \
    sudo apt-get install -y \
        git \
    && \
    sudo rm -rf \
        /tmp/* \
        /var/lib/apt/lists/* \
        /var/tmp/
