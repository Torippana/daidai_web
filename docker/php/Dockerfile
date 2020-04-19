FROM php:7.3-fpm-alpine
LABEL maintainer "makoto"

ARG TZ
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

RUN set -eux && \
  apk add --update-cache --no-cache --virtual=.build-dependencies tzdata && \
  apk add autoconf && \
  apk add build-base && \
  cp /usr/share/zoneinfo/${TZ} /etc/localtime && \
  apk del .build-dependencies && \
  docker-php-ext-install bcmath pdo_mysql && \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
  composer config -g repos.packagist composer https://packagist.jp && \
  composer global require hirak/prestissimo
RUN pecl install xdebug \
  && docker-php-ext-enable xdebug

# nodejs install
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apk add --update nodejs nodejs-npm
