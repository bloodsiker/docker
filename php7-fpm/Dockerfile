# See https://github.com/docker-library/php/blob/4677ca134fe48d20c820a19becb99198824d78e3/7.0/fpm/Dockerfile
FROM php:7.4-fpm

ARG TIMEZONE

MAINTAINER Maxence POUTORD <maxence.poutord@gmail.com>

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils \
    git \
    ssh \
    g++ \
    unzip \
    zlib1g-dev \
    libzip-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libssl-dev \
    libicu-dev \
    libonig-dev \
    apt-utils \
    nano \
    gnupg2 \
    && pecl channel-update pecl.php.net \
    && pecl install mongodb \
    && pecl install mcrypt-1.0.3 \ 
    && echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/ext-mongodb.ini \
    && echo "upload_max_filesize = 500M" > /usr/local/etc/php/conf.d/upload.ini

# RUN export PKG_CONFIG_PATH=/usr/lib/pkgconfig
RUN docker-php-ext-install iconv mbstring exif zip gd \
    && docker-php-ext-configure gd

# Install Composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Set timezone
#RUN rm /etc/localtime
#RUN ln -s /usr/share/zoneinfo/Europe/Kiev /etc/localtime
#RUN "date"
RUN ln -snf /usr/share/zoneinfo/Europe/Kiev /etc/localtime && echo "Europe/Kiev" > /etc/timezone
RUN printf '[PHP]\ndate.timezone = "%s";' Europe/Kiev > /usr/local/etc/php/conf.d/tzone.ini
RUN "date"

# mcrypt
RUN docker-php-ext-enable mcrypt

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install pdo pdo_mysql mysqli intl \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-install opcache

# install xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
RUN echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
RUN echo "upload_max_filesize=1G" >> /usr/local/etc/php/conf.d/upload.ini
RUN echo "memory_limit=512M" >> /usr/local/etc/php/conf.d/php.ini

# install nodejs 10.x
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get install -y nodejs

#RUN npm install npm@latest -g
RUN npm install -g semver

# bash aliases
RUN echo 'alias sf="php app/console"' >> ~/.bashrc
RUN echo 'alias sf3="php bin/console"' >> ~/.bashrc

# install libs for PDF generator
RUN apt-get install -y libxrender1 fontconfig libxext6 software-properties-common mc curl

# FFMPEG
#RUN echo "deb http://ftp.uk.debian.org/debian jessie-backports main" >> /etc/apt/sources.list \
#    && apt-get update && apt-get install -y ffmpeg
RUN apt-get install -y ffmpeg

# pip
RUN apt-get install -y python python-dev python-distribute python-pip

# redis
#RUN git clone -b php7-ipv6 https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \
RUN pecl install redis-5.1.0 && docker-php-ext-enable redis

# imagemagick
RUN apt-get update && apt-get install -y imagemagick libmagickwand-dev libmagickcore-dev \ 
	&& pecl install imagick && docker-php-ext-enable imagick

# image optimizers 
RUN apt-get install -y optipng jpegoptim

# yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update && apt-get install yarn

#amqp
RUN apt-get update && apt-get install -y librabbitmq-dev libssh-dev && docker-php-ext-install bcmath sockets \
    && pecl install amqp && docker-php-ext-enable amqp

#ADD /var/www/id_rsa /root/.ssh/id_rsa

WORKDIR /var/www