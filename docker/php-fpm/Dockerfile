FROM php:7-fpm

RUN apt-get clean && apt-get update && apt-get install -y --fix-missing --no-install-recommends \
    zlib1g-dev \
    libgeoip-dev \
    zip \
    unzip \
    make \
    curl \
    git \
    bash

RUN apt-get -y install gcc make autoconf libc-dev pkg-config

RUN apt-get -y install libssl-dev

RUN apt-get -y install librabbitmq-dev

RUN pecl install amqp

RUN docker-php-ext-install \
    pdo_mysql \
    gettext \
    mbstring \
    bcmath

COPY ./docker/php-fpm/php-custom.ini /usr/local/etc/php/conf.d/php-custom.ini

RUN curl --insecure https://getcomposer.org/composer.phar -o /usr/bin/composer && chmod +x /usr/bin/composer

COPY . /var/opt/application

WORKDIR /var/opt/application

RUN composer install
