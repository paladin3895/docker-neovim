FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive
ARG TARGET=v0.8.3


# Build nvim
# ARG BUILD_APT_DEPS="ninja-build gettext libtool libtool-bin autoconf automake cmake g++ pkg-config unzip git binutils"
# RUN apt update && apt upgrade -y && \
#   apt install -y ${BUILD_APT_DEPS}
# RUN git clone https://github.com/neovim/neovim.git /tmp/neovim && \
#   cd /tmp/neovim && \
#   git fetch --all --tags -f && \
#   git checkout ${TARGET} && \
#   make CMAKE_BUILD_TYPE=Release && \
#   make CMAKE_INSTALL_PREFIX=/usr/local install && \
#   strip /usr/local/bin/nvim

ARG BUILD_APT_UTILS="make wget curl git fzf"
RUN apt update && apt upgrade -y && \
  apt install -y ${BUILD_APT_UTILS}

# Install nvim
RUN wget --no-check-certificate "https://github.com/neovim/neovim/releases/download/stable/nvim-linux64.deb"
RUN dpkg -i ./nvim-linux64.deb

ENV NODE_VERSION=18.14.2
ENV NVM_DIR=/root/.nvm

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
ENV PATH="/root/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
RUN node --version
RUN npm --version

COPY ./config /root/.config

CMD ["/usr/bin/nvim"]
