# Download base image Ubuntu 18.04
FROM ubuntu:18.04

# Default directory
WORKDIR '/home'

# Update Ubuntu repositories
RUN apt-get update
RUN apt-get install -y --no-install-recommends apt-utils
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

# Install main programs
RUN apt-get install -y \
  nano \
  git

# Install and configure Oh My Zsh
RUN apt-get install -y zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
RUN cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
RUN sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="bira"/g' ~/.zshrc
RUN sed -i 's/  git/  z/g' ~/.zshrc
ENTRYPOINT executable /bin/zsh
