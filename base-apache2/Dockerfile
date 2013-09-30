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
RUN echo "
<VirtualHost *:80>
        ServerAdmin developers@some-site.com
        DocumentRoot /home
        UseCanonicalName Off

        RewriteEngine on

        RewriteMap lowercase int:tolower

        RewriteMap vhost txt:/home/vhost.map

        RewriteCond %{REQUEST_URI} !^/cgi-bin/
        RewriteCond ${lowercase:%{SERVER_NAME}} ^(.+)$
        RewriteCond ${vhost:%1} ^(/.*)$
        RewriteRule ^/(.*)$ %1/$1

        RewriteCond %{REQUEST_URI} ^/cgi-bin/
        RewriteCond ${lowercase:%{SERVER_NAME}} ^(.+)$
        RewriteCond ${vhost:%1} ^(/.*)$
        RewriteRule ^/(.*)$ %1/cgi-bin/$1

        ErrorLog /var/log/apache2/error.log

        # Possible values include: debug, info, notice, warn, error, crit,
        # alert, emerg.
        LogLevel alert

        CustomLog /var/log/apache2/access.log combined

</VirtualHost>
" > /etc/apache2/sites-enabled/default
RUN a2ensite default
RUN service apache2 restart

# Expose ports http, ssh
EXPOSE 8080
EXPOSE 22

