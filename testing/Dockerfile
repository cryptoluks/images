FROM docker.io/kalilinux/kali-last-release:latest

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin

ARG DEBIAN_FRONTEND=noninteractive

# Update
RUN <<-EOF
    echo "APT::Get::Assume-Yes true;" > /etc/apt/apt.conf.d/90assumeyes
    apt-get update
    apt-get dist-upgrade
    apt-get install \
      awscli \
      curl \
      fd-find \
      fzf \
      git \
      gitleaks \
      gnupg \
      iputils-ping \
      kali-tools-sniffing-spoofing \
      nuclei \
      pipenv \
      python3-poetry \
      ripgrep \
      screen \
      seclists \
      ssh-audit \
      testssl.sh \
      tmux \
      wget
    rm -rf /var/lib/apt/lists/*
EOF

# Install kali metapackages
RUN <<-EOF
    apt-get update
    apt-get install kali-linux-headless
    rm -rf /var/lib/apt/lists/*
EOF

RUN useradd -u 1000 -m -s /bin/bash -G sudo abcuser
RUN useradd -u 1001 -m -s /bin/bash -G sudo abcuser2
RUN usermod -aG root nobody
RUN usermod -aG shadow nobody
RUN mkdir -p /etc/sudoers.d
RUN echo "ALL ALL=(ALL) NOPASSWD: ALL" | tee /etc/sudoers.d/nopasswd
RUN echo abcuser:password | chpasswd
RUN echo abcuser2:password | chpasswd

USER 1001

SHELL ["/bin/sh", "-c"]
