# Basic site test
# outrunthewolf

# Base Docker File
FROM base/apache2

# ENVIRONMENTAL variables
ENV USERNAME username
ENV PASSWORD password
ENV SITENAME www.test.com
ENV SITEPATH "/home/$USERNAME/public_html"

ENV GIT_REMOTE_ORIGIN https://github.com/outrunthewolf/dockerfile-test.git
ENV GIT_BASE_FILES https://github.com/marcric/basic_html_test_page.git

# create a user
RUN useradd -d /home/$USERNAME -m $USERNAME
RUN chsh -s /bin/bash $USERNAME
RUN echo "$USERNAME:$PASSWORD" | chpasswd
RUN su $USERNAME
RUN cd /home/$USERNAME

# Set up a host in the apache2 vhost map
# vhosting is defined in the base apache2 setup
RUN echo $SITENAME $SITEPATH > /home/vhost.map

# Create some git stuff to bring in a repo if needs be
# these are examples, perform any manner of GIT/composer magic
RUN git init
RUN git remote add origin $GIT_REMOTE_ORIGIN
RUN git clone $GIT_BASE_FILES /home/$USERNAME