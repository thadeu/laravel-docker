FROM php:7.1.8-apache

MAINTAINER Thadeu Esteves Jr <dev@thadeu.work>

ENV APP_ROOT /srv/app
ENV DOCKER_PATH .docker

# Node.js
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
&& apt-get install -y nodejs && npm i npm@latest -g

RUN apt-get update && apt-get install -y libpng-dev

RUN npm install -g foreman cross-env

WORKDIR $APP_ROOT

ADD $DOCKER_PATH/vhost.conf /etc/apache2/sites-available/000-default.conf
ADD . .

RUN chown -R www-data:www-data . && a2enmod rewrite

RUN service apache2 restart

EXPOSE 8080
EXPOSE 80

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/*