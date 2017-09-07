FROM tetsuobe/php7

ENV BUILD_DEPS postgresql-dev


RUN apk update && apk add --no-cache --virtual .build-deps $BUILD_DEPS \
    && apk add --no-cache libpq \
    && docker-php-ext-install pdo_pgsql \
    && apk del .build-deps