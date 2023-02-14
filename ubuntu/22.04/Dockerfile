#syntax=docker/dockerfile:1.5.2

FROM ubuntu:22.04@sha256:9a0bdde4188b896a372804be2384015e90e3f84906b750c1a53539b585fbbe7f AS base

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
LABEL org.opencontainers.image.source="https://github.com/nicholasdille/docker-setup" \
      org.opencontainers.image.title="Ubuntu" \
      org.opencontainers.image.description="Base image for Ubuntu"