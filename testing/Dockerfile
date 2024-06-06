FROM docker.io/kalilinux/kali-last-release:latest

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin

ARG DEBIAN_FRONTEND=noninteractive

RUN useradd -u 1000 -m -s /bin/bash -G wheel abcuser

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

# Install pipx packages
RUN <<-EOF
    apt-get update
    apt-get install pipx
    pipx install azure-cli
    pipx install frida-tools
    pipx install objection
    pipx install semgrep
    pipx install http-prompt
    pipx install detect-secrets
    pipx install flawfinder
    rm -rf /var/lib/apt/lists/*
EOF

# Install Trivy
RUN <<-EOF
    apt-get update
    curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin
    rm -rf /var/lib/apt/lists/*
EOF

# Install Go
RUN <<-EOF
    apt-get update
    apt-get install golang
    rm -rf /var/lib/apt/lists/*
EOF

SHELL ["/bin/sh", "-c"]
