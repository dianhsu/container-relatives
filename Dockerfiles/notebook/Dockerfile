FROM ubuntu:21.04

ARG NB_USER="dianhsu"
ARG NB_UID="1000"
ARG NB_GID="100"

USER root
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN apt-get update && \ 
    apt-get install -y wget curl sudo locales zsh && \
    apt-get install -y vim python3 gcc g++ python3-pip  python-is-python3 && \
    apt-get install -y zip unzip git cmake && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN pip3 config set global.index-url https://mirrors.aliyun.com/pypi/simple/
RUN pip3 install jupyterlab requests numpy pandas pyyaml 
RUN useradd -ms /bin/bash $NB_USER
RUN usermod -aG sudo $NB_USER
WORKDIR /home/$NB_USER
RUN echo "$NB_USER	ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# ENV TINI_VERSION v0.19.0
# ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
# RUN chmod a+x /usr/bin/tini
# ENTRYPOINT ["/usr/bin/tini", "--"]


USER $NB_USER
RUN jupyter notebook --generate-config
RUN ls /home/${NB_USER}/.jupyter/
RUN echo 'c.NotebookApp.password = "argon2:$argon2id$v=19$m=10240,t=10,p=8$Kb03w1SIOAk2zmIgDXWAYw$fkvATu4iPI8LBBW9rzOjFw"' >> /home/$NB_USER/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.ip='0.0.0.0'" >> /home/$NB_USER/.jupyter/jupyter_notebook_config.py
RUN tail /home/$NB_USER/.jupyter/jupyter_notebook_config.py
RUN pip3 config set global.index-url https://mirrors.aliyun.com/pypi/simple/
CMD [ "jupyter", "notebook"]
