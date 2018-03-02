# 1 Download base image Ubuntu 18.04
FROM ubuntu:18.04

# 2 Manual setups
RUN mkdir ~/.local

# 3 Install main programs
RUN apt-get update && apt-get install -y \
  build-essential \
  nano \
  wget \
  git \
  subversion

# 4 Install LP Solve
RUN apt-get install -y lp-solve

# 5 Install and configure Coin-Or Linear Programming
RUN svn co https://projects.coin-or.org/svn/Clp/stable/1.16 /root/.local/coin-or-linear-programming
WORKDIR "/root/.local/coin-or-linear-programming"
RUN \
  ./configure -C && \
  make && \
  make test && \
  make install && \
  cp bin/clp /usr/local/bin

# 6 Generate solvers test
RUN mkdir /home/solvers_example
WORKDIR /home/solvers_example
RUN echo "NAME          EXLP7 \n\
ROWS \n\
 N  OBJ \n\
 G  GUB01 \n\
 L  ROW02 \n\
 E  ROW03 \n\
 G  ROW04 \n\
 L  ROW05 \n\
COLUMNS \n\
    COL01     OBJ                1.0 \n\
    COL01     GUB01              3.0   ROW05              5.6 \n\
    COL02     GUB01              1.0   ROW02              2.0 \n\
    COL03     OBJ                1.0 \n\
    COL03     ROW02              1.1   ROW03              1.0 \n\
    COL04     GUB01             -2.0   ROW04              2.8 \n\
    COL05     OBJ                2.0 \n\
    COL05     GUB01             -1.0   ROW05              1.0 \n\
    COL06     ROW03              1.0 \n\
    COL07     ROW04             -1.2 \n\
    COL08     OBJ               -1.0 \n\
    COL08     GUB01             -1.0   ROW05              1.9 \n\
RHS \n\
    RHS1      GUB01              2.5 \n\
    RHS1      ROW02              2.1 \n\
    RHS1      ROW03              4.0 \n\
    RHS1      ROW04              1.8 \n\
    RHS1      ROW05             15.0 \n\
RANGES \n\
    RNG1      ROW04              3.2 \n\
    RNG1      ROW05             12.0 \n\
BOUNDS \n\
 LO BND1      COL01              2.5 \n\
 UP BND1      COL02              4.1 \n\
 LO BND1      COL05              0.5 \n\
 UP BND1      COL05              4.0 \n\
 UP BND1      COL08              4.3 \n\
ENDATA" > example.mps
RUN echo "Linear Programming Test Commands\n\nCoin-Or Linear Programming\n> clp example.mps\n\nLP Solve\n> lp_solve -mps example.mps" > readme.txt

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
