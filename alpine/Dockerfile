FROM alpine:edge

LABEL maintainer="Dat Pham"

ARG BUILD_DEPS="bash git lua nodejs npm lazygit bottom python3 go neovim ripgrep alpine-sdk"
ARG TARGET=stable

COPY ./config/nvim/user.lua ~/.config/nvim/lua/user/init.lua

RUN apk add --no-cache ${BUILD_DEPS} --update && \
  git clone https://github.com/AstroNvim/AstroNvim ~/.config/nvim && \
  # Uncomment the line below and replace the link with your user config repo to load a user config
  # git clone https://github.com/username/AstroNvim_user ~/.config/nvim/lua/user
  nvim --headless -c "autocmd User PackerComplete quitall"

CMD ["/usr/bin/nvim"]
