FROM tylervigeant/ecomm-docker:m2-apache-1.0.5

RUN apt-get -y install libmagickwand-dev \
	&& printf "\n" | pecl install imagick \
	&& echo "extension=imagick.so" >> /usr/local/etc/php/conf.d/imagick.ini