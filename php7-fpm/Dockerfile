# See https://github.com/docker-library/php/blob/master/7.1/fpm/Dockerfile
FROM php:7.3-fpm
ARG TIMEZONE

MAINTAINER Shliakhov Sergey <shlyakhov.up@gmail.com>

RUN apt-get update && apt-get install -y \
    openssl \
    git \
    unzip

# Install Composer
# RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
# RUN composer --version

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone
RUN printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini
RUN "date"

RUN apt-get update && apt-get install -y libmcrypt-dev mariadb-client \
    libpng-dev \
    && docker-php-ext-install gd mbstring mysqli pdo pdo_mysql


RUN apt-get update && apt-get install -y procps

RUN usermod -u 1000 www-data

WORKDIR /var/www/app
RUN chown -R www-data:www-data /var/www/app
USER www-data

#RUN git clone https://github.com/laravel/laravel.git .
# RUN git clone https://pa_ku@bitbucket.org/punwave/yumau.git

# RUN composer install