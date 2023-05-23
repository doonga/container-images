ARG VERSION=latest@sha256:fc3948806b2f8c2826048a9ada51778651a158ce308778603435b9b9f571e8cd

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
