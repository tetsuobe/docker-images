FROM tetsuobe/docker-images:php7

MAINTAINER tetsuobe@gmail.com

ARG USER=root
ARG PASSWORD=root

ENV BUILD_DEPS \
                g++ \
                gcc \
                autoconf \
                make

RUN apk update && apk add --no-cache --virtual .build-deps $BUILD_DEPS git openssh \
    && docker-php-ext-install pdo_mysql \
    && pecl install -o xdebug \
    && docker-php-ext-enable xdebug \
    && sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
    && echo "${USER}:${PASSWORD}" | chpasswd \
    && ssh-keygen -A \
    && apk del .build-deps \
    && rm -rf /tmp/pear

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer \
    && composer global require "hirak/prestissimo" \
    && wget https://git.io/psysh \
    && chmod +x psysh \
    && mv psysh /usr/bin/psysh

ADD conf /etc/php7/conf.d/

EXPOSE 22 9000
