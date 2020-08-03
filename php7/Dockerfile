FROM php:7.4-fpm-alpine

LABEL maintainer="tetsuobe@gmail.com"

ENV BUILD_DEPS \
                zlib-dev \
                icu-dev \
                util-linux-dev \
                autoconf \
                g++ \
                gcc \
                make \
                pcre-dev \
                libzip-dev \
                oniguruma-dev

RUN apk update && apk add --no-cache --virtual .build-deps $BUILD_DEPS \
    && apk add bash icu-libs util-linux libzip \
    && docker-php-ext-install zip mbstring intl opcache bcmath \
    && pecl install -o apcu \
    && pecl install -o uuid \
    && docker-php-ext-enable apcu uuid \
    && apk del .build-deps \
    && rm -rf /tmp/pear

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer \
    && composer global require "hirak/prestissimo"

ADD conf /etc/php7/conf.d/

EXPOSE 9000