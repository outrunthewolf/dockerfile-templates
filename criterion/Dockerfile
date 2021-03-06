# Base Docker File
FROM outrunthewolf/nginx

# Criterion PHP CI Server
MAINTAINER outrunthewolf

ENV USERNAME criterion

# Install mongodb and driver
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/debian-sysvinit dist 10gen' >> /etc/apt/sources.list.d/mongodb.list

# Build some dependencies
RUN apt-get update
RUN apt-get install -y mongodb-10gen php-pear php5-dev
RUN pecl install mongo
RUN echo "extension=mongo.so" >> /etc/php5/cli/php.ini
RUN ephp5-fpm restart

# ENVIRONMENTAL variables
ENV USERNAME criterion
ENV SITEPATH "/home/$USERNAME/public_html"

# create a user
RUN useradd -d /home/$USERNAME -m $USERNAME
RUN chsh -s /bin/bash $USERNAME
RUN mkdir /home/$USERNAME/public_html

# Pull the repo
RUN git clone https://github.com/romhut/criterion.git /home/$USERNAME/public_html
RUN cd /home/$USERNAME/public_html && \
	composer install

# Add base nginx conf
ADD ./config/default_nginx_conf /usr/local/nginx/conf/nginx.conf

# Add a default vhost, activate host file
ADD ./config/default_vhost /usr/local/nginx/conf/sites-available/default.conf
RUN ln -s /usr/local/nginx/conf/sites-available/default.conf /usr/local/nginx/conf/sites-enabled/default.conf

# Set up php fpm, restart php
ADD ./config/default_php_pool /etc/php5/fpm/pool.d/default.conf
RUN touch /var/log/php-slowlog.log

# Expose some ports
EXPOSE 80

# Start it running
CMD service php5-fpm restart && \
	/usr/local/nginx/sbin/./nginx -c /usr/local/nginx/conf/nginx.conf





