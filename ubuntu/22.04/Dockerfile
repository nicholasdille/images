#syntax=docker/dockerfile:1.6.0

FROM ubuntu:22.04@sha256:c35ed11f8af26ef79671ab5536d90cdcf968d5d62f0f852b81f46f58b456fc2f AS base

SHELL [ "bash", "-o", "errexit", "-c"]
ARG DEBIAN_FRONTEND=noninteractive

COPY <<no-recommends <<no-suggests /etc/apt/apt.conf.d/
APT::Install-Recommends "false";
no-recommends
APT::Install-Suggests "false";
no-suggests

RUN <<EOF
grep security /etc/apt/sources.list >/etc/apt/sources.list.d/security.list
apt-get update -o Dir::Etc::SourceList=/etc/apt/false -o Dir::Etc::SourceParts=/etc/apt/sources.list.d
apt-get upgrade -y
rm -f /etc/apt/sources.list.d/security.list
EOF

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