FROM php:8.1-fpm-alpine3.16
COPY ./docker/fpm/php.ini /usr/local/etc/php/

RUN apk --no-cache update && \
    apk --no-cache upgrade && \
    apk --no-cache add \
    curl-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libxml2-dev \
    zlib-dev \
    pcre-dev \
    g++ \
    make \
    autoconf \
    openssl \
    nodejs \
    npm \
    bash \
    vim \
    git \
    oniguruma-dev \
    libzip-dev \
  && docker-php-ext-install \
    curl \
    dom \
    mbstring \
    pdo \
    pdo_mysql \
    simplexml \
    zip \
    opcache \
  && docker-php-ext-configure gd \
    --with-freetype=/usr/include/ \
    --with-jpeg=/usr/include/ \
  && docker-php-ext-install gd \
  && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  && chmod +x /usr/local/bin/composer \
  && rm -rf /var/cache/apk/* \
  && chown -R www-data ./ /var/www

WORKDIR /var/www
# RUN chown -R www-data ./ /var/www
USER www-data

COPY --chown=www-data:www-data . /var/www
RUN composer install --optimize-autoloader --no-dev && sh php artisan test

CMD ["sh", "-c", "php artisan config:cache --quiet; php artisan route:cache --quiet; php-fpm"]
