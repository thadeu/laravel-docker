FROM php:7.1.8-apache

MAINTAINER Thadeu Esteves Jr <dev@thadeu.work>

ENV APP_ROOT /srv/app
ENV DOCKER_PATH .docker

RUN apt-get update -qq && apt-get install -y \ 
  build-essential \
  libpq-dev \
  libpng-dev \
  postgresql-client-9.4 \
  mysql-client

# Node.js
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
&& apt-get install -y nodejs && npm i npm@latest -g

# cross-env global
RUN npm install -g cross-env

WORKDIR $APP_ROOT

ADD $DOCKER_PATH/vhost.conf /etc/apache2/sites-available/000-default.conf
ADD . .

RUN chown -R www-data:www-data . && a2enmod rewrite

RUN service apache2 restart

EXPOSE 80

# Clean up APT when done
RUN apt-get clean && rm -rf /var/lib/apt/lists/*