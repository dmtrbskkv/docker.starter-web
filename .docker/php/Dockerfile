FROM php:8.2-fpm

#ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
#RUN chmod +x /usr/local/bin/install-php-extensions && sync && \
#    install-php-extensions http

RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libonig-dev \
    libzip-dev \
    libmcrypt-dev \
    && docker-php-ext-install -j$(nproc) iconv mbstring mysqli pdo_mysql zip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Настройка пользователя для корректной работы
ENV USER=user USER_ID=1000 USER_GID=1000
RUN addgroup --gid ${USER_GID} ${USER}
RUN adduser --disabled-password --gecos '' --uid ${USER_ID} --gid ${USER_GID} ${USER}
USER ${USER}

