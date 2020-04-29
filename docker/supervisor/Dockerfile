FROM php:7.4.5-cli

RUN apt-get update \
    && apt-get install git zip unzip supervisor vim htop iputils-ping wget cron -y

RUN docker-php-ext-install pdo_mysql bcmath sockets

# install oh-my-zsh
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true
RUN echo "alias llq=\"ls -lah\"" >> ~/.zshrc

# install composer
RUN curl https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# create php.ini
COPY docker/supervisor/php.ini /usr/local/etc/php/php.ini

#supervisor
COPY docker/supervisor/supervisord.conf /etc/supervisor/supervisord.conf
COPY docker/supervisor/conf.d /etc/supervisor/conf.d
ENTRYPOINT supervisord -n -c /etc/supervisor/supervisord.conf

WORKDIR /src
