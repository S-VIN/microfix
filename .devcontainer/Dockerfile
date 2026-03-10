FROM ubuntu:24.04

ARG RUST_VERSION=stable
ARG USERNAME=dev
ARG USER_UID=1000
ARG USER_GID=1000

ENV DEBIAN_FRONTEND=noninteractive

# ── Базовые пакеты + GUI/X11 зависимости ──
RUN apt-get update && apt-get install -y --no-install-recommends \
    # базовое
    ca-certificates curl git sudo pkg-config cmake build-essential \
    # X11 / Wayland библиотеки для GUI
    libx11-dev libxcursor-dev libxrandr-dev libxinerama-dev libxi-dev \
    libxkbcommon-dev libwayland-dev libwayland-cursor0 libwayland-egl1 \
    libgl-dev libegl-dev libvulkan-dev \
    libfontconfig1-dev libfreetype-dev \
    # для отладки GUI (необязательно, но полезно)
    x11-utils mesa-utils \
    && rm -rf /var/lib/apt/lists/*

# ── Пользователь (UID/GID совпадают с хостом) ──
RUN groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd --uid ${USER_UID} --gid ${USER_GID} -m -s /bin/bash ${USERNAME} \
    && echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/${USERNAME}

USER ${USERNAME}
WORKDIR /home/${USERNAME}

# ── Rust ──
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y \
    --default-toolchain ${RUST_VERSION} \
    --component clippy rustfmt rust-analyzer

ENV PATH="/home/${USERNAME}/.cargo/bin:${PATH}"
