FROM docker.io/kalilinux/kali-last-release:latest

SHELL ["/bin/bash", "-euxo", "pipefail", "-c"]

ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin

ARG DEBIAN_FRONTEND=noninteractive

RUN useradd -u 1000 -m -s /bin/bash -G sudo abcuser
RUN useradd -u 1001 -m -s /bin/bash -G sudo abcuser2
RUN usermod -aG sudo nobody
RUN echo "ALL ALL=(ALL) NOPASSWD: ALL" | tee /etc/sudoers.d/nopasswd
RUN usermod -u 1002 nobody

USER 1001

SHELL ["/bin/sh", "-c"]
