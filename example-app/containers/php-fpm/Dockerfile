FROM phpdockerio/php73-fpm:latest

LABEL maintainer="Johan Frank"

WORKDIR "/application"

ARG WWWGROUP
ARG WWWUSER

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Add user to group
RUN groupadd --force -g $WWWGROUP wessla
RUN useradd -ms /bin/bash --no-user-group -g $WWWGROUP -u $WWWUSER wessla

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php7.3-mysql php7.3-redis php-xdebug php7.3-bcmath php7.3-gd php-imagick php7.3-intl php7.3-mbstring php7.3-dom \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install git (so we get Composer installed) (poor solution but works for now)
RUN apt-get update \
    && apt-get -y install git \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*