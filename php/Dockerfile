FROM php:7.1-fpm
COPY php.ini /usr/local/etc/php/

# php install
RUN apt-get update \
    && apt-get install -y zlib1g-dev libzip-dev default-mysql-client libicu-dev mariadb-client unzip \
    && docker-php-ext-install zip pdo_mysql intl

# php gd
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev libjpeg-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# composer install
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

WORKDIR /www

# RUN composer global require "laravel/installer"
