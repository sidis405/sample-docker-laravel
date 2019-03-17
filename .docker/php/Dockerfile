FROM php:7.1-fpm
LABEL maintainer="Sidrit Trandafili"

COPY .docker/php/composer/composer-installer.sh /usr/local/bin/composer-installer

RUN apt-get -yqq update \
    && apt-get -yqq install --no-install-recommends unzip \
    && chmod +x /usr/local/bin/composer-installer \
    && composer-installer \
    && mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer \
    && composer --version

WORKDIR /tmp
ADD composer.json composer.lock /tmp/
RUN mkdir -p database/seeds \
        mkdir -p database/factories \
        && composer install \
            --no-interaction \
            --no-plugins \
            --no-scripts \
            --prefer-dist \
        && rm -rf composer.json composer.lock auth.json \
        database/ vendor/

COPY . /var/www/html/
WORKDIR /var/www/html/
COPY .docker/php/php.ini /usr/local/etc/php/php.ini
RUN chown -R www-data:www-data /var/www/html

RUN composer install \
        --no-interaction \
        --no-plugins \
        --no-scripts \
        --prefer-dist
