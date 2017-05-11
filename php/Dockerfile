#
# php 7.0 with fpm enabled
#
# extra enabled extensions:
#   bcmath calendar pdo_mysql zip opcache grpc gd mcrypt
#
FROM php:7.0-fpm

RUN apt-get update \
    && apt-get install -y \
        git \
        wget \
        rake \
        ruby-ronn \
        libmemcached-dev \
        zlib1g-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && apt-get clean \
    && docker-php-ext-install -j$(nproc) mcrypt \
    && docker-php-ext-install -j$(nproc) bcmath \
    && docker-php-ext-install -j$(nproc) calendar \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-configure zip --enable-zip \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install -j$(nproc) opcache \

    && pecl install memcached grpc \
    && docker-php-ext-enable memcached grpc \

# vim:ft=dockerfile
