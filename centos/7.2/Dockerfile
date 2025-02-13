FROM fulcrum/centos7
MAINTAINER IF Fulcrum "fulcrum@ifsight.net"

# Enable EPEL Repos, update, install PHP 5.6, postdrop correct perms, add the user
RUN echo "Cache bust PHP 5.6.37" && \
    yum --noplugins install -y \
        https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
        http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    yum --noplugins --enablerepo=remi,remi-php56 -y install php php-fpm php-gd php-imap php-ldap php-mbstring php-mysql php-opcache php-pgsql php-soap php-xml php-mcrypt php-pecl-redis php-php-gettext postfix && \
    yum --noplugins upgrade -y && \
    package-cleanup --dupes && \
    package-cleanup --cleandupes && \
    yum clean all && \
    rm -rf /var/cache/yum && \
    sed -i '/^listen = /clisten = 0.0.0.0:9000' /etc/php-fpm.d/www.conf && \
    sed -i '/^listen.allowed_clients/c;listen.allowed_clients =' /etc/php-fpm.d/www.conf && \
    sed -i '/^;catch_workers_output/ccatch_workers_output = yes' /etc/php-fpm.d/www.conf && \
    chmod g+s /usr/sbin/postqueue /usr/sbin/postdrop && \
    groupadd -g 1971 php && useradd -d /var/www/html -g php -M -n -s /sbin/nologin -u 1971 php

ENTRYPOINT ["/usr/sbin/php-fpm"]
CMD ["--nodaemonize"]
