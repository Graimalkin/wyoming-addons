FROM debian:bookworm-slim
ARG TARGETARCH
ARG TARGETVARIANT

# Install openWakeWord
WORKDIR /usr/src
ARG WYOMING_OPENWAKEWORD_VERSION='v1.10.0'
ARG REPO_OWNER='rhasspy'

RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        python3 \
        python3-pip \
        python3-venv \
        libopenblas0 \
    \
    && python3 -m venv .venv \
    && .venv/bin/pip3 install --no-cache-dir -U \
        setuptools \
        wheel \
    && .venv/bin/pip3 install --no-cache-dir \
        --extra-index-url https://www.piwheels.org/simple \
        "wyoming-openwakeword @ https://github.com/${REPO_OWNER}/wyoming-openwakeword/archive/refs/tags/${WYOMING_OPENWAKEWORD_VERSION}.tar.gz" \
    \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /
COPY run.sh ./

EXPOSE 10400

ENTRYPOINT ["bash", "/run.sh"]
