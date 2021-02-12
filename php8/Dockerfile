FROM composer:latest AS composer

FROM php:8.0-fpm-alpine

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
    && apk add bash icu-libs util-linux libzip openssh acl \
    && docker-php-ext-install zip mbstring intl opcache bcmath \
    && pecl install -o apcu \
    && pecl install -o uuid \
    && docker-php-ext-enable apcu uuid \
    && apk del .build-deps \
    && rm -rf /tmp/pear

COPY --from=composer /usr/bin/composer /usr/bin/composer

ADD conf /etc/php7/conf.d/

EXPOSE 22 9000
