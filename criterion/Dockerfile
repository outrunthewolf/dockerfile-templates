# Base Ubuntu 12.04 Image
# Apache2, php5, composer, mongodb
# outrunthewolf

# Base Docker File
FROM ubuntu:precise

# Check we've got the lastest distr
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list

# Update the box
RUN apt-get update

# Install any programs needed, including composer
RUN apt-get install -y git-core apache2 php5 libapache2-mod-php5 nano htop openssh-server curl
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/bin/composer

# Set up the vhosting for apache2 and enable any mods
RUN a2enmod rewrite
RUN echo "VARIOUS BITS AND BOBS" > /etc/apache2/sites-enabled/default
RUN service apache2 restart

# git clone criterion
RUN mkdir /home/sites
RUN git clone https://github.com/romhut/criterion.git /home/sites/criterion
RUN cd /home/sites/criterion
RUN composer install && bin/cli install

# Set up a host in the apache2 vhost map
# vhosting is defined in the base apache2 setup
RUN echo $SITENAME $SITEPATH > /home/vhost.map

# Restart apache


