FROM scratch

ADD openwrt-x86-64-generic-rootfs.tar.gz /

EXPOSE 80

RUN mkdir /var/lock && \
    opkg update && \
    opkg install uhttpd-mod-lua && \
    uci set uhttpd.main.interpreter='.lua=/usr/bin/lua' && \
    uci commit uhttpd


USER root

CMD ["/sbin/init"]

