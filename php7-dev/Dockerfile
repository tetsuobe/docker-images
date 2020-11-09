FROM tetsuobe/docker-images:php7

LABEL maintainer="tetsuobe@gmail.com"

ARG USER=root
ARG PASSWORD=root

ENV BUILD_DEPS \
                g++ \
                gcc \
                autoconf \
                make

RUN apk update && apk add --no-cache --virtual .build-deps $BUILD_DEPS \
    && apk add git \
    && pecl install -o xdebug \
    && docker-php-ext-enable xdebug \
    && apk del .build-deps \
    && rm -rf /tmp/pear

RUN sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
    && echo "${USER}:${PASSWORD}" | chpasswd \
    && ssh-keygen -A

ADD conf /usr/local/etc/php/conf.d/

EXPOSE 9000
