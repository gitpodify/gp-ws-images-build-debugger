# [Choice] Node.js version (use -bullseye variants on local arm64/Apple Silicon): 18, 16, 14, 18-bullseye, 16-bullseye, 14-bullseye, 18-buster, 16-buster, 14-buster
ARG VARIANT="18-bullseye"
FROM mcr.microsoft.com/vscode/devcontainers/universal:linux as builder
USER root

# Magic DNS in a container where /etc/resolv.conf is a bind mount needed
# extra support, currently on a development branch.
WORKDIR /go/src/tailscale
RUN git clone https://github.com/tailscale/tailscale.git && cd tailscale && \
    go mod download && \
    go install -mod=readonly ./cmd/tailscaled ./cmd/tailscale

# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.233.0/containers/javascript-node/.devcontainer/base.Dockerfile

FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT}

COPY --from=builder /go/bin/tailscaled /usr/sbin/tailscaled
COPY --from=builder /go/bin/tailscale /usr/bin/tailscale
COPY overlay/ /

# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "source /usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node modules
# RUN su node -c "npm install -g <your-package-list-here>"
