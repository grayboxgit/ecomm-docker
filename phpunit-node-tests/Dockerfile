FROM alpine:3.11

RUN apk upgrade \
  && apk add wget \
             curl \
             git \
             npm \
             bash \
             dnsmasq \
             patch \
             libsodium-dev \
             yarn \
             busybox-suid \
             php7 \
             php7-curl \
             php7-intl \
             php7-json \
             php7-mbstring \
             php7-openssl \
             php7-pdo_mysql \
             php7-pdo_pgsql \
             php7-pdo_sqlite \
             php7-phar \
             php7-xml \
             php7-zlib \
             php7-session \
             php7-fileinfo \
             apache2 \
             supervisor \
             php7-apache2 \
             php7-simplexml \
             php7-iconv \
             php7-ctype \
             php7-mcrypt \
             php7-gd \
             php7-xml \
             php7-dom \
             php7-xdebug \
             php7-bcmath \
             php7-xsl \
             php7-zip \
             php7-tokenizer \
             php7-xmlwriter \
             php7-soap \
             php7-sodium \
             php7-opcache \
             php7-sockets \
             php7-imagick

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.10.20

RUN npm install glob file-eval --save --quiet