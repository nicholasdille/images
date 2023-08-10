#syntax=docker/dockerfile:1.5.2

FROM ubuntu:22.04@sha256:67211c14fa74f070d27cc59d69a7fa9aeff8e28ea118ef3babc295a0428a6d21 AS base

SHELL [ "bash", "-o", "errexit", "-c"]

COPY <<no-recommends <<no-suggests /etc/apt/apt.conf.d/
APT::Install-Recommends "false";
no-recommends
APT::Install-Suggests "false";
no-suggests

RUN --mount=type=cache,sharing=private,target=/var/lib/apt/lists \
    --mount=type=cache,sharing=private,target=/var/cache \
    --mount=type=cache,sharing=private,target=/var/log \
    --mount=type=cache,sharing=private,target=/usr/lib/python3/dist-packages/__pycache__ \
    <<EOF
apt-get update
apt-get -y install \
    git \
    curl \
    ca-certificates \
    jq \
    unzip \
    binutils \
    xz-utils \
    less \
    vim-tiny
rm /usr/local/sbin/unminimize
EOF

ARG ref=main
LABEL org.opencontainers.image.source="https://github.com/nicholasdille/images" \
      org.opencontainers.image.title="Ubuntu" \
      org.opencontainers.image.description="Base image for Ubuntu"