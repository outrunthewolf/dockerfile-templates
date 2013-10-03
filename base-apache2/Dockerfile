# Base Ubuntu 12.04 Image
# Apache2, php5, composer
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
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

RUN a2enmod rewrite

# Create the mass vhost
ADD ./config/default_vhost /etc/apache2/sites-enabled/default

# touch the local vhost
RUN touch /home/vhost.map

# enable the default site
RUN a2ensite default

# restart apache
RUN service apache2 restart

# Expose ports http, ssh
EXPOSE 80

# Make sure the container is running something
ENTRYPOINT ["/usr/sbin/apache2"]
CMD ["-D", "FOREGROUND"]

