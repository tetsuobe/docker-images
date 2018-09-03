FROM php:7.2-fpm-alpine

MAINTAINER tetsuobe@gmail.com

ENV BUILD_DEPS \
                zlib-dev \
                icu-dev \
                util-linux-dev \
                autoconf \
                g++ \
                gcc \
                make \
                pcre-dev

RUN apk update && apk add --no-cache --virtual .build-deps $BUILD_DEPS \
    && apk add bash icu-libs util-linux \
    && docker-php-ext-install zip mbstring intl opcache bcmath \
    && pecl install -o apcu \
    && pecl install -o uuid \
    && docker-php-ext-enable apcu uuid \
    && apk del .build-deps \
    && rm -rf /tmp/pear

EXPOSE 9000