FROM fballiano/magento2-apache-php

RUN apt-get install -y sudo curl software-properties-common
RUN curl -sL https://deb.nodesource.com/setup_11.x | sudo bash -
RUN apt update || apt update
RUN apt-get install -y nodejs
RUN apt-get install -y npm
RUN npm install -g grunt-cli