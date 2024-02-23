# Créer un Dockerfile pour cette application en mode production
FROM php:fpm-alpine3.19

WORKDIR /var/www/symfony

COPY . /var/www/symfony

ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apk add zlib-dev g++ git icu-dev zip libzip-dev zip \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- \
     --install-dir=/usr/bin --filename=composer


RUN composer install --no-dev --optimize-autoloader



RUN php bin/console asset-map:compile

RUN php bin/console cache:clear --env=prod