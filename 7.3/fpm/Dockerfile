####################################
# PHPDocker.io PHP 7.3 / FPM image #
####################################

FROM registry.lab.jalameta.co.id/images/php/cli:7.3

# Install FPM
RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get -y --no-install-recommends install php7.3-fpm \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# PHP-FPM packages need a nudge to make them docker-friendly
COPY overrides.conf /etc/php/7.3/fpm/pool.d/z-overrides.conf

# PHP-FPM has really dirty logs, certainly not good for dockerising
# The following startup script contains some magic to clean these up
COPY php-fpm-startup /usr/bin/php-fpm
CMD /usr/bin/php-fpm
