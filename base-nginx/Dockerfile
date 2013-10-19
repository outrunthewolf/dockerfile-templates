# Base Ubuntu 12.04 Image
# Nginx, php5, composer, mysql
# outrunthewolf

# Base Docker File
FROM ubuntu:precise

# ENVIRONMENTAL variables
ENV USERNAME chris
ENV PASSWORD password
ENV SITENAME outrunthewolf.com
ENV SITEPATH "/home/$USERNAME/public_html"

# create a user
RUN useradd -d /home/$USERNAME -m $USERNAME
RUN chsh -s /bin/bash $USERNAME
RUN echo "$USERNAME:$PASSWORD" | chpasswd

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
	mkdir /usr/local/nginx/conf/sites-enabled && \
	echo "include sites-enabled/default.conf;" > /usr/local/nginx/conf/nginx.conf

# Add a default vhost
ADD ./config/default_vhost /usr/local/nginx/sites-available/default.conf
RUN ln -s 

# Set up php fpm


# Expose some ports
