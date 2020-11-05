FROM tetsuobe/docker-images:php7

LABEL maintainer="tetsuobe@gmail.com"

ENV BUILD_DEPS \
                g++ \
                gcc \
                autoconf \
                make

RUN apk update && apk add --no-cache --virtual .build-deps $BUILD_DEPS git \
    && pecl install -o xdebug \
    && docker-php-ext-enable xdebug \
    && apk del .build-deps \
    && rm -rf /tmp/pear

ADD conf /usr/local/etc/php/conf.d/

EXPOSE 9000
