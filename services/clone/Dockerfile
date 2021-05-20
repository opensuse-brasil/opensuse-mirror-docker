FROM registry.opensuse.org/opensuse/leap:latest

RUN zypper in -y rsync

ENV RSYNC_SERVER="rsync.opensuse.org"
ENV RSYNC_MODULE="opensuse-full-with-factory"
ENV RSYNC_USER="opensuse"
ENV RSYNC_PASSWORD=""
ENV RSYNC_CHOWN="1000:1000"

RUN mkdir -p /srv/pub/opensuse

VOLUME ["/srv/pub/opensuse", "/var/log/"]

STOPSIGNAL SIGTERM

RUN ln -sf /dev/stdout /var/log/rsync.log

CMD rsync -rlpt ${RSYNC_USER}@${RSYNC_SERVER}::${RSYNC_MODULE}/opensuse/ /srv/pub/opensuse/ \
          --include-from=/etc/rsync-include.txt \
          --delete-after \
          --delete-excluded \
          --max-delete=4000 \
          --timeout=1800 \
          --log-file=/var/log/rsync.log \
          --owner \
          --group \
          --chown=${RSYNC_CHOWN} \
          -hi
