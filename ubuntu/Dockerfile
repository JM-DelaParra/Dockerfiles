# Download base image Ubuntu 18.04
FROM ubuntu:18.04

# Update Ubuntu repositories
RUN apt-get update

# Manual setups
RUN mkdir ~/.local

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
RUN touch ~/.z

# Default directory
WORKDIR '/home'

# Start with zsh
RUN /bin/zsh
ENTRYPOINT /bin/zsh
