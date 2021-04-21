FROM registry.opensuse.org/opensuse/leap:latest

RUN zypper in -y rsync

ENV RSYNC_SERVER="rsync.opensuse.org"
ENV RSYNC_MODULE="opensuse-full-with-factory"
ENV RSYNC_USER="opensuse"
ENV RSYNC_PASSWORD=""

RUN groupadd mirror
RUN useradd -m -g mirror -c "openSUSE Mirror User" -s /bin/bash mirror

RUN mkdir -p /srv/pub/opensuse
RUN chown -R mirror:mirror /srv/pub/opensuse

VOLUME ["/srv/pub/opensuse"]

STOPSIGNAL SIGTERM

USER mirror:mirror

CMD rsync -rlpt ${RSYNC_USER}@${RSYNC_SERVER}::${RSYNC_MODULE}/opensuse/ /srv/pub/opensuse/ \
          --include-from=/etc/rsync-include.txt \
          --delete-after \
          --delete-excluded \
          --max-delete=4000 \
          --timeout=1800 \
          -hi
