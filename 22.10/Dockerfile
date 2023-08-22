#docker run -v C:\:/CTF --privileged -p 23946:23946 -it pwn:22.10
FROM ubuntu:22.10
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ Asia/Seoul
ENV PYTHONIOENCODING UTF-8
ENV LC_CTYPE C.UTF-8
WORKDIR /root

RUN apt update && apt install -y netcat-traditional
RUN apt install vim git gcc ssh curl wget gdb sudo zsh python3 python3-pip libffi-dev build-essential libssl-dev libc6-i386 libc6-dbg gcc-multilib make -y
RUN apt install -y qemu-system qemu-kvm
RUN apt install -y python-is-python3
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
RUN echo "source ~/pwndbg/gdbinit.py\nsource ~/Pwngdb/pwngdb.py\nsource ~/Pwngdb/angelheap/gdbinit.py\ndefine hook-run\npython\nimport angelheap\nangelheap.init_angelheap()\nend\nend" >> ~/.gdbinit

# REMOTE DEBUGGING
EXPOSE 23946
RUN apt install ruby-full -y
RUN gem install one_gadget seccomp-tools

RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true
RUN mkdir -p "$HOME/.zsh"
RUN git clone https://github.com/sindresorhus/pure.git "$HOME/.zsh/pure"
RUN echo "fpath+=("$HOME/.zsh/pure")\nautoload -U promptinit; promptinit\nprompt pure" >> ~/.zshrc

RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
RUN echo "source ~/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc

RUN git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
RUN echo "source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
RUN echo "ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=111'" >> ~/.zshrc
RUN git clone https://github.com/msh1307/init
WORKDIR /root/init
RUN /root/init/go.sh
WORKDIR /root
RUN apt install qemu-user-static file
