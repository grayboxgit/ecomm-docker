FROM fballiano/magento2-apache-php

RUN rm -rf /var/lib/apt/lists/*
RUN apt update || apt update
RUN apt-get update || apt-get update

RUN apt-get install -y sudo nano curl software-properties-common
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo bash -
RUN apt-get install -y nodejs
RUN npm install -g grunt-cli

## Keep this chunk at the bottom!
RUN echo "deb http://deb.debian.org/debian stretch-backports main" >> /etc/apt/sources.list
RUN apt update || apt update
RUN apt-get -t stretch-backports --assume-yes install "libsodium-dev"
RUN docker-php-ext-install sodium