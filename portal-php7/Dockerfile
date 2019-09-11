# Build php-image
FROM php:7.1-fpm-alpine

# Add build dependencies to virtual group
RUN apk --no-cache --virtual temp add build-base \
                       autoconf && \
    apk --no-cache add zeromq-dev \
                       libxml2-dev \
                       composer \
                       sox \
                       git && \
    pecl install zmq-beta && \
    docker-php-ext-enable zmq && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install soap && \
    docker-php-ext-install pcntl && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install opcache && \
    docker-php-ext-install sockets && \
    apk del temp

RUN composer global require hirak/prestissimo && \
    sed -e 's/mysqli.reconnect = Off/mysqli.reconnect = On/' -i /etc/php7/php.ini && \
    sed -e 's/max_execution_time = 30/max_execution_time = 60/' -i /etc/php7/php.ini

ENV TZ=Europe/Amsterdam

RUN apk --update add \
    tzdata \
  && cp /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Fix iconv on alpinelinux
RUN apk add --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/community gnu-libiconv
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

EXPOSE 9000