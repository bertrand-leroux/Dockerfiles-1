FROM jmleroux/php:5.6
MAINTAINER JM Leroux <jmleroux.pro@gmail.com>

# Define "root" as current user
USER root

# Install PHP FPM
RUN apt-get update && \
    apt-get --no-install-recommends --no-install-suggests --yes --quiet install php5-fpm && \
    apt-get clean && apt-get --yes --quiet autoremove --purge && \
    rm -rf  /var/lib/apt/lists/* /tmp/* /var/tmp/* \
            /usr/share/doc/* /usr/share/groff/* /usr/share/info/* /usr/share/linda/* \
            /usr/share/lintian/* /usr/share/locale/* /usr/share/man/*

# Configure PHP FPM
RUN sed -i "s/;date.timezone =/date.timezone = Etc\/UTC/" /etc/php5/fpm/php.ini

RUN sed -i "s/user = www-data/user = docker/" /etc/php5/fpm/pool.d/www.conf && \
    sed -i "s/group = www-data/group = docker/" /etc/php5/fpm/pool.d/www.conf && \
    sed -i "s/listen.owner = www-data/listen.owner = docker/" /etc/php5/fpm/pool.d/www.conf && \
    sed -i "s/listen.group = www-data/listen.group = docker/" /etc/php5/fpm/pool.d/www.conf

RUN php5dismod xdebug

RUN sed -i "s/listen = .*/listen = 9001/" /etc/php5/fpm/pool.d/www.conf

# Define "docker" as current user
USER docker

# Run FPM in foreground
CMD ["sudo", "php5-fpm", "-F"]
