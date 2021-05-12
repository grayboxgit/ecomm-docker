FROM tylervigeant/ecomm-docker:m2-apache-1.3.0

RUN apt-get install -y curl software-properties-common
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo bash -
RUN apt-get install -y nodejs \
    && npm install -g grunt-cli

CMD ["/start.sh"]
