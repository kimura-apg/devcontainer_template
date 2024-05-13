FROM node:latest

# Install needed packages
RUN apt-get update && apt-get install -y \
  git \
  gh \
  zsh \
  && rm -rf /var/lib/apt/lists/*

# Install pnpm
RUN npm install -g pnpm@9.1.0
RUN pnpm config set store-dir /home/node/.local/share/pnpm/store

# Install Oh My Zsh and plugins
RUN sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)" "" --unattended
RUN git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

RUN sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/' ~/.zshrc
RUN echo "ZSH_HIGHLIGHT_STYLES[command]='fg=green'" >> ~/.zshrc
RUN echo "ZSH_HIGHLIGHT_STYLES[unknown-token]='fg=red'" >> ~/.zshrc

# Set zsh as default shell
RUN chsh -s $(which zsh)

WORKDIR /workspace

# Set environment variables
ENV SHELL /bin/zsh
ENV PNPM_HOME /workspace/.pnpm

CMD ["zsh"]
