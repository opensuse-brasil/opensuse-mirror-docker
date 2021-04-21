FROM registry.opensuse.org/opensuse/leap:latest

RUN zypper in -y rsync

COPY rsyncd.conf /etc/rsyncd.conf

EXPOSE 873

STOPSIGNAL SIGTERM

RUN ln -sf /dev/stdout /var/log/rsyncd.log

CMD ["rsync", "--daemon", "--no-detach"]
