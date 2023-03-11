FROM ubuntu:22.10
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ Asia/Seoul
ENV PYTHONIOENCODING UTF-8
ENV LC_CTYPE C.UTF-8
WORKDIR /root
# RUN sed -i -r 's/([a-z]{2}.)?archive.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
# RUN sed -i -r 's/security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
RUN apt update && apt upgrade -y
RUN apt-get install netcat-traditional -y
RUN apt install vim git gcc ssh curl wget gdb sudo zsh python3 python3-pip libffi-dev build-essential libssl-dev libc6-i386 libc6-dbg gcc-multilib make -y
RUN dpkg --add-architecture i386
RUN apt update
RUN apt install libc6:i386 -y
RUN python3 -m pip install --upgrade pip
RUN pip3 install unicorn
RUN pip3 install keystone-engine
RUN pip3 install pwntools
RUN pip3 install ropgadget
RUN apt install libcapstone-dev -y
RUN git clone https://github.com/pwndbg/pwndbg
WORKDIR pwndbg
RUN ./setup.sh
WORKDIR /root
RUN echo source ~/pwndbg/gdbinit.py >> ~/.gdbinit

RUN apt install ruby-full -y
RUN gem install one_gadget seccomp-tools

RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true
RUN mkdir -p "$HOME/.zsh"
RUN git clone https://github.com/sindresorhus/pure.git "$HOME/.zsh/pure"
RUN echo "fpath+=("$HOME/.zsh/pure")\nautoload -U promptinit; promptinit\nprompt pure" >> ~/.zshrc

RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
RUN echo "source ./zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc

RUN git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
RUN echo "source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
RUN echo "ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=111'" >> ~/.zshrc