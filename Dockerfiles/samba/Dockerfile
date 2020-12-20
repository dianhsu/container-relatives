FROM alpine

ARG NB_USER="dianhsu"
ARG NB_UID="1000"

USER root
ENV TZ=Asia/Shanghai
ENV SHELL=/bin/bash
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apk add --update \
    samba-common-tools \
    samba-client \
    samba-server \
    && rm -rf /var/cache/apk/*

RUN useradd -ms /bin/bash -u $NB_UID $NB_USER
RUN usermod -aG sudo $NB_USER
WORKDIR /home/$NB_USER
RUN echo "$NB_USER	ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

EXPOSE 445/tcp

ENTRYPOINT ["smbd", "--foreground", "--log-stdout"]
CMD []