# Basic site test
# outrunthewolf

# Base Docker File, inherit apache2
FROM base/apache2

# ENVIRONMENTAL variables
ENV USERNAME local.docker.com
ENV PASSWORD password
ENV SITENAME local.docker.com
ENV SITEPATH "/home/$USERNAME/public_html"
ENV GIT_BASE_FILES https://github.com/marcric/basic_html_test_page.git

# create a user
RUN useradd -d /home/$USERNAME -m $USERNAME
RUN chsh -s /bin/bash $USERNAME
RUN echo "$USERNAME:$PASSWORD" | chpasswd

# Set up a host in the apache2 vhost map
# vhosting is defined in the base apache2 setup
RUN echo $SITENAME $SITEPATH > /home/vhost.map

# Create some git stuff to bring in a repo if needs be
# these are examples, perform any manner of GIT/composer magic
