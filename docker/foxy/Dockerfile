# Dockerfile
FROM ubuntu:20.04
LABEL author="Steve Jeong"
LABEL e-mail="how2soft@gmail.com"
LABEL gihtub="how2flow"
LABEL version="0.0.1"

ARG DEBIAN_FRONTEND=noninteractive

# shell: bash
SHELL ["/bin/bash", "-c"]

ENV USER="user" \
  PASSWORD="docker" \
  GITCONFIG="https://raw.githubusercontent.com/how2flow/config/ubuntu/gitconfig" \ 
  TMUXCONFIG="https://raw.githubusercontent.com/how2flow/config/ubuntu/tmux.conf" \
  VIMCONFIG="https://raw.githubusercontent.com/how2flow/config/ubuntu/vimrc" \
  VIMCOLORS="https://raw.githubusercontent.com/morhetz/gruvbox/master/colors/gruvbox.vim"

# root user fixups
USER root
WORKDIR /root
COPY preinst preinst
COPY packages packages
COPY user user
RUN chmod +x preinst packages user && \
  ./preinst && rm preinst && \
  ./packages && rm packages && \
  ./user $USER && rm user

# normal user fixups
USER $USER
WORKDIR /home/$USER
COPY postinst postinst
RUN echo $PASSWORD | sudo -S chmod +x postinst && \
  ./postinst && rm postinst
RUN mkdir -p ~/robot_ws/src && \
  mkdir -p .vim/colors && \
  mkdir -p .vim/bundle
RUN wget -O .gitconfig --no-check-certificate $GITCONFIG && \
  wget -O .tmux.conf --no-check-certificate $TMUXCONFIG && \
  wget -O .vimrc --no-check-certificate $VIMCONFIG && \
  wget -O .vim/colors/gruvbox.vim --no-check-certificate $VIMCOLORS
RUN git clone "https://github.com/VundleVim/Vundle.vim.git" \
  .vim/bundle/Vundle.vim
RUN vim +PluginInstall +qall
RUN echo "alias tmux='tmux -2'" >> .bashrc
RUN echo "set -o vi" >> .bashrc
