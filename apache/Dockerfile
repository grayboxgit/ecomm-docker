FROM fballiano/magento2-apache-php

RUN apt-get install $PHPIZE_DEPS \
	&& pecl install xdebug-2.7.1 \

RUN apt-get install -y sudo nano