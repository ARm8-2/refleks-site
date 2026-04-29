FROM debian:bookworm-slim

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl git ca-certificates build-essential \
    sudo bash-completion locales \
    && sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen \
    && locale-gen \
    && rm -rf /var/lib/apt/lists/*

ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

ARG USERNAME=vscode
RUN groupadd --gid 1000 $USERNAME \
    && useradd --uid 1000 --gid 1000 -m -s /bin/bash $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && cp /etc/skel/.bashrc /home/$USERNAME/.bashrc \
    && chown $USERNAME:$USERNAME /home/$USERNAME/.bashrc

RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - && \
    apt-get install -y nodejs && \
    rm -rf /var/lib/apt/lists/*

USER $USERNAME
ENV HOME=/home/$USERNAME

WORKDIR /workspaces/refleks-index
