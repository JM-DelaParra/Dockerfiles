# 1 Download base image Ubuntu 18.04
FROM ubuntu:18.04

# 2 Manual setups
RUN mkdir ~/.local

# 3 Install main programs
RUN apt-get update && apt-get install -y \
  software-properties-common \
  nano \
  git

# 4 Install Java
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer && \
  java -version > /home/software.vesion 2>&1 && \
  javac -version >> /home/software.vesion 2>&1

# 5 Install Scala
RUN \
  echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list && \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823 && \
  apt-get update && apt-get install -y sbt=1.1.1 && \
  sbt sbtVersion

# 6 Get test files
RUN \
  mkdir /home/test_files && \
  git clone https://github.com/JM-DelaParra/Test-Files.git /home/test_files && \
  rm -r /home/test_files/.git && \
  rm /home/test_files/README.md

# n-2 Install and configure Oh My Zsh (install all with bash first for compatibility)
RUN  \
  apt-get update && apt-get install -y zsh && \
  git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh && \
  cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc && \
  sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="bira"/g' ~/.zshrc && \
  sed -i 's/  git/  z/g' ~/.zshrc && \
  touch ~/.z && \
  /bin/zsh

# n-1 Default directory
WORKDIR /home

# n Start with zsh
ENTRYPOINT /bin/zsh
