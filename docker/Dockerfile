FROM php:7.4-apache
COPY ./php/php.ini /usr/local/etc/php/
COPY ./apache/*.conf /etc/apache2/sites-enabled/

RUN apt-get update \
    && apt-get install -y \
    libpq-dev \
    mariadb-client \
    unzip \
    vim \
    git \
    && docker-php-ext-install zip pdo_mysql mysqli \
    && docker-php-ext-enable mysqli

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

WORKDIR /var/www/html

#RUN sed -i 's!/var/www/html!/var/www/html/public!g' /etc/apache2/sites-available/000-default.conf
RUN  a2enmod rewrite
RUN composer global require "laravel/installer"
