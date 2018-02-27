# Download base image Ubuntu 18.04
FROM ubuntu:18.04

# Update Ubuntu repositories
RUN apt-get update

# Manual setups
RUN mkdir ~/.local
RUN touch ~/.z

# Install main programs
RUN apt-get install -y \
  build-essential \
  nano \
  git \
  subversion

# Install and configure Oh My Zsh
RUN apt-get install -y zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
RUN cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
RUN sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="bira"/g' ~/.zshrc
RUN sed -i 's/  git/  z/g' ~/.zshrc

# Install and configure Coin-Or Linear Programming
RUN svn co https://projects.coin-or.org/svn/Clp/stable/1.16 /root/.local/coin-or-linear-programming
WORKDIR "/root/.local/coin-or-linear-programming"
RUN ./configure -C
RUN make
RUN make test
RUN make install
WORKDIR "/root/.local/coin-or-linear-programming/Clp/examples"
RUN make DRIVER=hello
RUN ./hello

# Default directory
WORKDIR '/home'

# Start with zsh
RUN /bin/zsh
ENTRYPOINT /bin/zsh
