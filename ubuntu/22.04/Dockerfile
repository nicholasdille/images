#syntax=docker/dockerfile:1.5.1

FROM ubuntu:22.04@sha256:f05532b6a1dec5f7a77a8d684af87bc9cd1f2b32eab301c109f8ad151b5565d1 AS base

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