FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential pkg-config cmake curl ca-certificates git sudo \
    libx11-dev libxcursor-dev libxrandr-dev libxinerama-dev libxi-dev \
    libxkbcommon-dev libwayland-dev libwayland-cursor0 libwayland-egl1 \
    libgl-dev libegl-dev libvulkan-dev \
    libfontconfig1-dev libfreetype-dev \
    x11-utils mesa-utils \
    && rm -rf /var/lib/apt/lists/*

USER ubuntu

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

ENV PATH="/home/ubuntu/.cargo/bin:${PATH}"
