FROM php:7.2-fpm

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        nano \
        libjpeg62-turbo-dev \
        libpng-dev \
        libmcrypt-dev \
        libicu-dev \
        libxml2-dev \
        git \
        zip \
        unzip \
    && pecl install xdebug-2.8.1 \
    && docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/  --with-jpeg-dir=/usr/include/  --with-png-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd mysqli pdo pdo_mysql intl opcache \
    && docker-php-ext-enable xdebug gd \
    && mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /application

CMD ["php-fpm"]