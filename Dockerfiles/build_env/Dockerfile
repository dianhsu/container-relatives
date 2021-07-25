FROM ubuntu:devel

ENV TZ=UTC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y gcc g++ cmake build-essential git curl wget vim zip unzip sudo rsync mkisofs

RUN apt-get install -y asciidoc binutils bzip2 flex gawk help2man intltool libelf-dev zlib1g-dev make libncurses5-dev libssl-dev patch perl-modules python2-dev gettext xsltproc
ARG B_USER="dianhsu"
ARG B_UID="1001"

RUN useradd -ms /bin/bash -u $B_UID $B_USER
RUN usermod -aG sudo $B_USER

RUN echo "$B_USER	ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

WORKDIR /home/$B_USER

USER $B_USER

RUN mkdir ~/workspace

CMD []


