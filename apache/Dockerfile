FROM fballiano/magento2-apache-php

RUN apt-get install $PHPIZE_DEPS \
	&& pecl install xdebug-2.7.1 \
	&& docker-php-ext-enable xdebug

RUN apt-get install -y sudo nano