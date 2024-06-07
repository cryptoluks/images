FROM docker.io/kalilinux/kali-last-release:latest

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin

ARG DEBIAN_FRONTEND=noninteractive

RUN useradd -u 1000 -m -s /bin/bash -G sudo abcuser
RUN useradd -u 1001 -m -s /bin/bash -G sudo abcuser2
RUN usermod -aG root nobody
RUN usermod -aG shadow nobody
RUN mkdir -p /etc/sudoers.d
RUN echo "ALL ALL=(ALL) NOPASSWD: ALL" | tee /etc/sudoers.d/nopasswd
RUN echo abcuser:password | chpasswd
RUN echo abcuser2:password | chpasswd
RUN mv /bin/grep /bin/grep-original
RUN cat <<EOF > /bin/grep
#!/usr/bin/env bash
if [ $(id -u) -eq 0 ]; then
  touch /tmp/grep-test
fi
/bin/grep-original "$@"
EOF
RUN chmod 755 /bin/grep


SHELL ["/bin/sh", "-c"]
