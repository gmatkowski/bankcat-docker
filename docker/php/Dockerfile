# Image
FROM php:8.0-fpm

# Starting from scratch
RUN apt-get clean
RUN apt-get -y autoremove
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# PS
RUN apt-get update && apt-get install -y procps

# Dependencies
RUN apt-get update

# Zip
RUN apt-get install -y libzip-dev zip && docker-php-ext-configure zip && docker-php-ext-install zip

# Git
RUN apt-get install -y git

# NANO
RUN apt-get install -y nano

# Curl
RUN apt-get install -y libcurl3-dev curl && docker-php-ext-install curl

# HTOP
RUN apt-get install -y htop

# ImageMagick
RUN apt-get install -y imagemagick && apt-get install -y --no-install-recommends libmagickwand-dev
RUN pecl install imagick && docker-php-ext-enable imagick

# PostgreSQL
RUN apt-get install -y libpq-dev && docker-php-ext-install pdo pdo_pgsql

# BC Math
RUN docker-php-ext-install bcmath

# PHP Other extensions
RUN docker-php-ext-install exif && docker-php-ext-enable exif

# PHP Redis extension
RUN pecl install redis
RUN docker-php-ext-enable redis

# Composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer
RUN chmod 0755 /usr/bin/composer

# Laravel NEW
RUN composer global require laravel/installer

# Phpunit global
RUN composer global require phpunit/phpunit

# PHP Sockets
RUN docker-php-ext-install sockets

# PHP GD
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd

#OPCACHE
RUN docker-php-ext-install opcache

# NPM & PM2
RUN apt-get install npm -y
RUN npm install pm2 -g

# PHP Intl
RUN docker-php-ext-install intl

# ENV PATH
ENV PATH=~/.composer/vendor/bin:$PATH
ENV PATH=/var/www/bin:$PATH

# Composer keys
COPY ./composer /root/.composer

# Custom php.ini config
COPY configs/php.ini /usr/local/etc/php/php.ini

# Clean up
RUN apt-get clean
RUN apt-get -y autoremove
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set up default directory
WORKDIR /var/www
