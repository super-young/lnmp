FROM php:7.2-fpm
RUN mkdir /app
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd mysqli pdo pdo_mysql
RUN apt-get update && apt-get install -y libmemcached-dev zlib1g-dev \
    && pecl install memcached-3.1.4 \
    && pecl install xdebug-2.6.0 \
    && docker-php-ext-enable memcached mysqli \
    && docker-php-ext-enable mysqli \
    && docker-php-ext-enable pdo \
    && docker-php-ext-enable pdo_mysql \
    && docker-php-ext-enable xdebug
ADD ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
EXPOSE 9000
CMD ["php-fpm"]