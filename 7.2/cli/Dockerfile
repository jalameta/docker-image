####################################
# PHPDocker.io PHP 7.2 / CLI image #
####################################

FROM ubuntu:focal

ARG DEBIAN_FRONTEND=noninteractive

# Fixes some weird terminal issues such as broken clear / CTRL+L
ENV TERM=linux

# Install Ondrej repos for Ubuntu Bionic, PHP7.2, composer and selected extensions - better selection than
# the distro's packages
RUN apt-get update \
    && apt-get install -y --no-install-recommends gnupg \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu focal main" > /etc/apt/sources.list.d/ondrej-php.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C \
    && apt-get update \
    && apt-get update \
    && apt-get -y --no-install-recommends install dialog apt-utils curl ca-certificates unzip sqlite3 libsqlite3-dev \
        openssh-server git\
        php7.2-cli \
        php7.2-curl \
        php7.2-apcu \
        php7.2-apcu-bc \
        php7.2-bcmath \
        php7.2-mysql \
        php7.2-pgsql \
        php7.2-redis \
        php7.2-gd \
        php7.2-json \
        php7.2-mbstring \
        php7.2-opcache \
        php7.2-readline \
        php7.2-xml \
        php7.2-zip \
        php7.2-sqlite3 \
        php7.2-soap \
        php7.2-xdebug \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require laravel/envoy \
    && composer clear-cache \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* 

RUN ln -s /root/.composer/vendor/laravel/envoy/bin/envoy /usr/bin/envoy

CMD ["php", "-a"]

# If you'd like to be able to use this container on a docker-compose environment as a quiescent PHP CLI container
# you can /bin/bash into, override CMD with the following - bear in mind that this will make docker-compose stop
# slow on such a container, docker-compose kill might do if you're in a hurry
# CMD ["tail", "-f", "/dev/null"]
