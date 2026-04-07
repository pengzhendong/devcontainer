FROM ubuntu:24.04
LABEL org.opencontainers.image.source https://github.com/pengzhendong/devcontainer
LABEL maintainer="Zhendong Peng <zhendong.peng@qq.com>"

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
  autojump ca-certificates coreutils curl ffmpeg fzf \
  gawk git locales net-tools rsync sox sudo tmux \
  tmux-mem-cpu-load vim wget zip zsh \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

ARG USERNAME=pengzhendong.pzd
RUN useradd -m $USERNAME -s /bin/zsh -g root \
  && echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER $USERNAME
WORKDIR /home/$USERNAME

RUN curl -fsSL \
  "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh" \
  -o Miniforge3-$(uname)-$(uname -m).sh \
  && sh Miniforge3-$(uname)-$(uname -m).sh -b \
  && rm Miniforge3-$(uname)-$(uname -m).sh
RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
RUN /bin/bash -c "$(curl -fsSL get.chezmoi.io)" -- init --apply pengzhendong \
  && wait="" /bin/zsh ~/.zshrc

ENV TERM=xterm-256color
ENV DEBIAN_FRONTEND=dialog
CMD ["zsh"]
