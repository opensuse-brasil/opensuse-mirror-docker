FROM registry.opensuse.org/opensuse/leap:15.3

RUN zypper addrepo https://download.opensuse.org/repositories/server:http/openSUSE_Leap_15.3/server:http.repo
RUN zypper -n --no-gpg-checks refresh
RUN zypper in -y nginx nginx-module-fancyindex nginx-module-geoip2 nginx-module-headers-more

COPY nginx.conf /etc/nginx/nginx.conf
COPY fancyindex /srv/www/fancyindex

VOLUME ["/srv/www/fancyindex", "/var/log/"]

EXPOSE 80 443

STOPSIGNAL SIGTERM

RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

CMD nginx -g 'daemon off;'
