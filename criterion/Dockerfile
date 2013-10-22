# Base Ubuntu 12.04 Image
# Apache2, php5, composer, mongodb
# outrunthewolf
MAINTAINER outrunthewolf

# Base Docker File
FROM outrunthewolf/nginx

# Install mongodb and driver
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/debian-sysvinit dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list

# Build some dependencies
RUN apt-get update
RUN apt-get install -y mongodb-10gen
RUN pecl install mongo

# Create a user and folder 


