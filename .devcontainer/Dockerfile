FROM mcr.microsoft.com/devcontainers/base:debian

# Install basic development tools and iptables/ipset
RUN apt-get update && apt-get install -y --no-install-recommends \
  sudo \
  git \
  iptables \
  ipset \
  iproute2 \
  dnsutils \
  aggregate \
  jq \
  vim \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

ARG USERNAME=vscode

# Set `DEVCONTAINER` environment variable to help with orientation
ENV DEVCONTAINER=true

# Create workspace and config directories and set permissions
RUN mkdir -p /workspace && \
  chown -R vscode:vscode /workspace

WORKDIR /workspace

# Set up non-root user
USER vscode

# Copy and set up firewall script
COPY init-firewall.sh /usr/local/bin/
USER root
RUN chmod +x /usr/local/bin/init-firewall.sh && \
  echo "vscode ALL=(root) NOPASSWD: /usr/local/bin/init-firewall.sh" > /etc/sudoers.d/vscode-firewall && \
  chmod 0440 /etc/sudoers.d/vscode-firewall
USER vscode
