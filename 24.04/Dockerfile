FROM ubuntu:24.04

ENV LANG=C.UTF-8
ENV LANGUAGE=C.UTF-8
ENV LC_ALL=C.UTF-8
WORKDIR /root

RUN apt update

# For pwntools, one_gadget, zsh package
RUN apt install python3 python3-pip git libssl-dev libffi-dev build-essential zsh -y

# etc tools
RUN apt install unzip curl gdb gcc g++ iputils-ping make vim net-tools ssh tmux wget file -y

# pwntools install
RUN python3 -m pip install --upgrade pip --break-system-packages --ignore-installed
RUN python3 -m pip install --upgrade pwntools --break-system-packages --ignore-installed

# install pwndbg
WORKDIR /root
RUN git clone https://github.com/pwndbg/pwndbg
WORKDIR /root/pwndbg
RUN git checkout 2023.03.19
RUN ./setup.sh

# install one_gadget
WORKDIR /root
RUN apt install ruby ruby-dev -y
RUN gem install elftools -v 1.1.3
RUN gem install one_gadget -v 1.9.0

# zsh setting
RUN chsh -s $(which zsh) 
RUN zsh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
RUN sed -i 's|ZSH_THEME="robbyrussell"|ZSH_THEME="awesomepanda"|g' ~/.zshrc
RUN git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
RUN sed -i 's|plugins=(git)|plugins=(git zsh-syntax-highlighting zsh-autosuggestions)|g' ~/.zshrc
RUN echo 'ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE="fg=cyan"' >> ~/.zshrc

CMD ["zsh"]