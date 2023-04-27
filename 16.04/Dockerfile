FROM ubuntu:16.04

ARG DEBIAN_FRONTEND=noninteractive

ENV TZ Asia/Seoul
ENV PYTHONIOENCODING UTF-8
ENV LC_CTYPE C.UTF-8

WORKDIR /root
RUN echo "deb [arch=amd64] http://archive.ubuntu.com/ubuntu/ xenial main restricted multiverse universe" > /etc/apt/sources.list
RUN echo "deb-src [arch=amd64] http://archive.ubuntu.com/ubuntu/ xenial main restricted multiverse universe" > /etc/apt/sources.list
RUN echo "deb [arch=amd64] http://archive.ubuntu.com/ubuntu/ xenial-updates main restricted multiverse universe" >> /etc/apt/sources.list
RUN echo "deb [arch=amd64] http://archive.ubuntu.com/ubuntu/ xenial-security main restricted multiverse universe" >> /etc/apt/sources.list
RUN echo "deb-src [arch=amd64] http://archive.ubuntu.com/ubuntu/ xenial-updates main restricted multiverse universe" >> /etc/apt/sources.list
RUN echo "deb-src [arch=amd64] http://archive.ubuntu.com/ubuntu/ xenial-security main restricted multiverse universe" >> /etc/apt/sources.list
RUN apt update
RUN apt install -y netcat
RUN apt update && apt install vim git gcc ssh curl wget gdb zsh python3 python3-dev python3-pip libffi-dev build-essential libssl-dev libc6-i386 libc6-dbg gcc-multilib make -y

RUN dpkg --add-architecture i386
RUN apt update
RUN apt install libc6:i386 -y

RUN pip3 install unicorn
RUN pip3 install keystone-engine
RUN pip3 install -U pip==20.3.4
RUN pip3 install -U pwntools
RUN pip3 install capstone ropper
RUN pip3 install ropgadget
RUN apt install libcapstone-dev -y

RUN wget https://github.com/hugsy/gef/archive/refs/tags/2020.03.tar.gz
RUN tar -xzvf 2020.03.tar.gz
RUN echo source ~/gef-2020.03/gef.py >> ~/.gdbinit

RUN apt install ruby-full -y
RUN apt install ruby-dev -y
RUN gem install one_gadget -v 1.7.3

RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true
RUN mkdir -p "$HOME/.zsh"
RUN git clone https://github.com/sindresorhus/pure.git "$HOME/.zsh/pure"
RUN echo "fpath+=("$HOME/.zsh/pure")\nautoload -U promptinit; promptinit\nprompt pure" >> ~/.zshrc

RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
RUN echo "source ./zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc

RUN git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
RUN echo "source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
RUN echo "ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=111'" >> ~/.zshrc
