FROM ubuntu:bionic

ARG USER_ID=1024
ARG GROUP_ID=1024

RUN bash
RUN apt-get update --fix-missing
RUN apt-get upgrade -y

RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:neovim-ppa/stable

RUN apt-get update -y
RUN apt-get install -y build-essential
RUN apt-get install -y pkg-config
RUN apt-get install -y neovim
RUN apt-get install -y libssl-dev
RUN apt-get install -y openssl
RUN apt-get install -y python-dev python-pip python3-dev python3-pip
RUN apt-get install -y net-tools htop wget curl git

RUN add-apt-repository ppa:x4121/ripgrep
RUN apt-get update -y
RUN apt-get install -y ripgrep

RUN pip install --no-cache-dir tensorflow==2.0.0-alpha0 

#add group
RUN addgroup --gid $GROUP_ID dev-group

#node user
RUN useradd -u $USER_ID --gid $GROUP_ID -ms /bin/bash default

#mv config files
ADD . /home/default/Config
ADD init.vim /home/default/.config/nvim/init.vim
ADD bashrc /home/default/.bashrc
ADD profile /home/default/.profile

#permissions
RUN chown -R default /home/default/.config
RUN chown default /home/default/.config/nvim
RUN chmod a+x /home/default/.config/nvim

RUN chown default /home/default/.config/nvim/init.vim
RUN chmod a+x /home/default/.config/nvim/init.vim

RUN chown default /home/default/.profile
RUN chmod a+x /home/default/.profile

RUN chown default /home/default/.bashrc
RUN chmod a+x /home/default/.bashrc

USER default
WORKDIR /home/default

RUN mkdir /home/default/Applications

RUN wget https://nodejs.org/dist/v11.12.0/node-v11.12.0-linux-x64.tar.xz
RUN chmod a+x ./node-v11.12.0-linux-x64.tar.xz
RUN unxz ./node-v11.12.0-linux-x64.tar.xz
RUN tar -xf ./node-v11.12.0-linux-x64.tar
RUN mv ./node-v11.12.0-linux-x64 /home/default/Applications/node
RUN chown default /home/default/Applications/node
RUN chmod u+x+w /home/default/Applications/node/*
RUN rm -rf ./node-v11.12.0-linux-x64.tar

CMD ["bash"]
