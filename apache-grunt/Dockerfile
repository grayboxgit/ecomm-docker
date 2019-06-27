FROM fballiano/magento2-apache-php

RUN echo "deb http://deb.debian.org/debian stretch-backports main" >> /etc/apt/sources.list
RUN apt update || apt update
RUN apt-get -t stretch-backports --assume-yes install "libsodium-dev"
RUN docker-php-ext-install sodium

RUN apt-get install -y sudo curl software-properties-common
RUN curl -sL https://deb.nodesource.com/setup_11.x | sudo bash -
RUN apt-get install -y nodejs
RUN apt-get install -y npm
RUN npm install -g grunt-cli