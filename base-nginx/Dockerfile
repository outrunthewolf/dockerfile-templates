# Base Ubuntu 12.04 Image
# Nginx, php5, composer
# outrunthewolf

# Base Docker File
FROM ubuntu:precise

# Maintainer
MAINTAINER outrunthewolf

# ENVIRONMENTAL variables
ENV USERNAME john
ENV PASSWORD password
ENV SITENAME whatever.com
ENV SITEPATH "/home/$USERNAME/public_html"

# create a user
RUN useradd -d /home/$USERNAME -m $USERNAME
RUN chsh -s /bin/bash $USERNAME
RUN echo "$USERNAME:$PASSWORD" | chpasswd
RUN mkdir /home/$USERNAME/public_html

# Check we've got the lastest distr
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list

# Update the box
RUN apt-get update

# Install any programs needed, including composer
RUN apt-get install -y git-core php5 php5-fpm php5-cgi php5-cli spawn-fcgi curl php5-curl php5-mcrypt nano htop openssh-server gcc libpcre3 libpcre3-dev libssl-dev make
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/bin/composer

# Download and install nginx
RUN cd /home/$USERNAME && \
	mkdir downloads && \
	cd downloads && \
	wget http://nginx.org/download/nginx-1.4.1.tar.gz && \
	tar -zxvf nginx-1.4.1.tar.gz && \
	cd nginx-1.4.1 && \
	./configure --with-http_ssl_module --user=$USERNAME && \
	make && \
	make install

# Set up nginx configurations
RUN mkdir /usr/local/nginx/conf/sites-available && \
	mkdir /usr/local/nginx/conf/sites-enabled

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
