# Python cloud-native development environment
# Based on python:3.12 and aligned with TradingAgents latest changes

FROM python:3.12

# Install code-server and common extensions.
# The latest upstream commit removed humao.rest-client on purpose.
RUN curl -fsSL https://code-server.dev/install.sh | sh \
  && code-server --install-extension cnbcool.cnb-welcome \
  && code-server --install-extension redhat.vscode-yaml \
  && code-server --install-extension dbaeumer.vscode-eslint \
  && code-server --install-extension waderyan.gitblame \
  && code-server --install-extension mhutchie.git-graph \
  && code-server --install-extension donjayamanne.githistory \
  && code-server --install-extension ms-python.python \
  && code-server --install-extension golang.go \
  && code-server --install-extension tencent-cloud.coding-copilot \
  && echo done

# Install system dependencies and ssh service for remote IDE access.
RUN apt-get update && apt-get install -y \
  git wget unzip openssh-server curl ca-certificates gnupg

# Install uv package manager.
ENV UV_INSTALL_DIR="/usr/local/bin"
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

# Install latest Node.js LTS 22.x.
RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
  && apt-get install -y nodejs

# Install Go 1.24.
RUN wget -q https://go.dev/dl/go1.24.0.linux-amd64.tar.gz -O /tmp/go.tar.gz \
  && tar -C /usr/local -xzf /tmp/go.tar.gz \
  && rm /tmp/go.tar.gz
ENV PATH="/usr/local/go/bin:${PATH}"
ENV GOPATH="/go"
ENV PATH="${GOPATH}/bin:${PATH}"

# UTF-8 locale support.
ENV LANG C.UTF-8
ENV LANGUAGE C.UTF-8
