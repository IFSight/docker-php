FROM fulcrum/alpine
MAINTAINER IF Fulcrum "fulcrum@ifsight.net"






RUN echo '@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories && \
    apk update && apk upgrade && \
    apk add php5 php5-ctype php5-curl php5-dom php5-fpm php5-ftp php5-gd php5-gettext php5-imap php5-json php5-ldap php5-mcrypt php5-mysql php5-mysqli php5-opcache php5-openssl php5-pdo php5-pdo_mysql php5-redis@testing php5-soap php5-sockets php5-xml php5-zlib php5-zip postfix && \
    adduser -h /var/www/html -s /sbin/nologin -D -H -u 1971 php && \
    chown -R postfix  /var/spool/postfix                        && \
    chgrp -R postdrop /var/spool/postfix/public                 && \
    chgrp -R postdrop /var/spool/postfix/maildrop               && \
    chown -R root     /var/spool/postfix/pid                    && \
    chown    root     /var/spool/postfix                        && \
    echo smtputf8_enable = no >> /etc/postfix/main.cf


ENTRYPOINT ["/usr/bin/php-fpm"]

CMD ["--nodaemonize"]
