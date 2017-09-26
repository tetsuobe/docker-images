FROM tetsuobe/php7

ENV BUILD_DEPS \
				autoconf \
				g++ \
				openssl-dev \
				make \
				pcre-dev

RUN apk update && apk add --no-cache --virtual .build-deps $BUILD_DEPS \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb \
    && apk del .build-deps