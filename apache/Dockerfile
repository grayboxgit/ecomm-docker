FROM fballiano/magento2-apache-php

RUN apt-get install -y sudo nano

RUN apt-get install $PHPIZE_DEPS \
    && pecl install xdebug-2.7.1

RUN apt-get -y install libmagickwand-dev \
	&& printf "\n" | pecl install imagick \
	&& echo "extension=imagick.so" >> /usr/local/etc/php/conf.d/imagick.ini

RUN echo "deb http://deb.debian.org/debian stretch-backports main" >> /etc/apt/sources.list
RUN apt update || apt update
RUN apt-get -t stretch-backports --assume-yes install "libsodium-dev"
RUN docker-php-ext-install sodium