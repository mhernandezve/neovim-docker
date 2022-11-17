FROM python:3.9

ARG USER_ID
ARG GROUP_ID

ENV TERM xterm

RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		neovim \
    tmux \
    silversearcher-ag \
		bat \
		fonts-powerline \
		tmuxinator \
		locales \
	; \
	rm -rf /var/lib/apt/lists/*

# Set the locale
RUN sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# set up user and environment
# RUN addgroup --gid $GROUP_ID user && \
#   adduser --disabled-password --gecos '' --uid $USER_ID --gid $GROUP_ID user

# RUN chsh -s /usr/bin/zsh user 
# USER user
# ENV HOME /home/user

# Copy dotfiles
RUN curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

RUN curl -fLo ~/.config/nvim/init.vim --create-dirs \
		https://raw.githubusercontent.com/mhernandezve/dotfiles/master/nvim/.config/nvim/init.vim

RUN curl -fLo ~/.tmux.conf \
		https://raw.githubusercontent.com/mhernandezve/dotfiles/master/tmux/.tmux.conf

# Install Neovim plugins
RUN vim +'PlugInstall --sync' +qa

RUN echo $USER_ID
