FROM mcr.microsoft.com/devcontainers/typescript-node:1-22-bullseye

# Install additional system packages
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    curl \
    wget \
    git \
    ca-certificates \
    gnupg \
    lsb-release \
    mosquitto \
    mosquitto-clients

# Install step-cli with architecture-specific logic
ARG TARGETARCH
RUN if [ "$TARGETARCH" = "amd64" ]; then \
    wget -O /tmp/step.deb https://dl.smallstep.com/gh-release/cli/gh-release-header/v0.28.7/step-cli_0.28.7-1_amd64.deb; \
    elif [ "$TARGETARCH" = "arm64" ]; then \
    wget -O /tmp/step.deb https://dl.smallstep.com/gh-release/cli/gh-release-header/v0.28.7/step-cli_0.28.7-1_arm64.deb; \
    else \
    echo "Unsupported architecture: $TARGETARCH" && exit 1; \
    fi \
    && dpkg -i /tmp/step.deb \
    && rm /tmp/step.deb