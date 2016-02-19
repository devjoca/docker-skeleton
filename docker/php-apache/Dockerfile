FROM php:5.6-apache

#install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

#install mod rewrite
RUN a2enmod rewrite
RUN service apache2 restart

RUN usermod -u 1000 www-data

RUN export TERM=xterm

#install common apache exntensions
RUN apt-get update && apt-get install -y \
        git-core \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd pdo zip
