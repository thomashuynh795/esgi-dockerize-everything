# Créer un Dockerfile pour cette application en mode production
FROM php:8.3-fpm

WORKDIR /var/www/symfony

COPY . /var/www/symfony

ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apt update \
    && apt install -y zlib1g-dev g++ git libicu-dev zip libzip-dev zip \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- \
     --install-dir=/usr/bin --filename=composer

RUN wget https://get.symfony.com/cli/installer -O - | bash

RUN composer install --no-dev --optimize-autoloader

RUN composer require symfony/runtime

RUN php bin/console asset-map:compile

RUN php bin/console cache:clear --env=prod