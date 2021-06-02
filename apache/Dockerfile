FROM php:7.4-apache

RUN apt-get update \
  && apt-get install -y \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxslt1-dev \
    git \
    vim \
    wget \
    lynx \
    psmisc \
  && apt-get clean

RUN set -eux; \
    docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg; \
    docker-php-ext-configure intl; \
    docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd; \
    docker-php-ext-install -j "$(nproc)" \
        gd \
        intl \
        opcache \
        pdo_mysql \
        xsl \
        bcmath \
        soap \
        sockets 
RUN apt-get install -y zip libzip-dev \
  && docker-php-ext-configure zip \
  && docker-php-ext-install zip

ADD https://raw.githubusercontent.com/colinmollenhour/credis/master/Client.php /credis.php
ADD https://raw.githubusercontent.com/fballiano/docker-magento2-apache-php/master/php.ini /usr/local/etc/php/conf.d/888-fballiano.ini
ADD https://raw.githubusercontent.com/fballiano/docker-magento2-apache-php/master/register-host-on-redis.php /register-host-on-redis.php
ADD https://raw.githubusercontent.com/fballiano/docker-magento2-apache-php/master/unregister-host-on-redis.php /unregister-host-on-redis.php
ADD https://raw.githubusercontent.com/fballiano/docker-magento2-apache-php/master/start.sh /start.sh

RUN usermod -u 1000 www-data; \
  a2enmod rewrite; \
  curl -o /tmp/composer-setup.php https://getcomposer.org/installer; \
  curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig; \
  php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"; \
  php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --version=1.10.22; \
  rm /tmp/composer-setup.php; \
  chmod +x /usr/local/bin/composer; \
  composer self-update --1; \
  curl -o n98-magerun2.phar http://files.magerun.net/n98-magerun2-latest.phar; \
  chmod +x ./n98-magerun2.phar; \
  chmod +x /start.sh; \
  chmod +r /credis.php; \
  mv n98-magerun2.phar /usr/local/bin/; \
  mkdir -p /root/.composer

RUN apt-get install -y sudo nano

## bin/magento support:backup:db support
RUN apt-get install -y mariadb-client-10.3 lsof

## grunt support
RUN apt-get install -y ncat

RUN apt-get install $PHPIZE_DEPS \
    && pecl install xdebug-2.9.6

RUN apt update || apt update
RUN apt-get install libsodium-dev
RUN docker-php-ext-install sodium

RUN apt-get install -y libmagickwand-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick

CMD ["/start.sh"]
