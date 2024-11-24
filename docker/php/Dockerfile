FROM docker.io/php:8.2-fpm
COPY php.ini /usr/local/etc/php

USER root

RUN useradd php

RUN apt update \
    && apt install -y zlib1g-dev mariadb-client vim libzip-dev \
    && docker-php-ext-install zip pdo_mysql

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER=1
ENV COMPOSER_HOME=/composer
ENV PATH=$PATH:/composer/vendor/bin

WORKDIR /var/www

RUN composer global require "laravel/installer"

USER php
