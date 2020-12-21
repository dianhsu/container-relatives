FROM ubuntu

ARG NB_USER="dianhsu"
ARG NB_UID="1000"

USER root
ENV TZ=Asia/Shanghai
ENV SHELL=/bin/bash
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget curl sudo locales iputils-ping zsh libgl-dev libglib2.0-0 vim python3 gcc g++ python3-pip  python-is-python3 && \
    apt-get install -y zip unzip git cmake && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN pip3 install jupyterlab requests numpy pandas pyyaml matplotlib
RUN useradd -ms /bin/bash -u $NB_UID $NB_USER
RUN usermod -aG sudo $NB_USER
WORKDIR /home/$NB_USER
RUN echo "$NB_USER	ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# ENV TINI_VERSION v0.19.0
# ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
# RUN chmod a+x /usr/bin/tini
# ENTRYPOINT ["/usr/bin/tini", "--"]


RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

USER $NB_USER
RUN echo "PATH=$PATH:/home/${NB_USER}/.local/bin" >> /home/${NB_USER}/.bashrc
RUN pip3 config set global.index-url https://mirrors.aliyun.com/pypi/simple/
ENTRYPOINT [ "bash", "-c", "jupyter notebook --ip=0.0.0.0 --no-browser"]
