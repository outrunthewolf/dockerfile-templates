# Basic site test
# Chris Roach

# Base Docker File
FROM base/apache2

# ENV variables
ENV USERNAME username
ENV PASSWORD password

ENV GIT_REMOTE_ORIGIN https://github.com/outrunthewolf/dockerfile-test.git
ENV GIT_BASE_FILES https://github.com/marcric/basic_html_test_page.git

# create a user
RUN useradd -d /home/$USERNAME -m $USERNAME
RUN chsh -s /bin/bash $USERNAME
RUN echo "$USERNAME:$PASSWORD" | chpasswd
RUN su $USERNAME

# Create some git shizzle
RUN cd
RUN git init
RUN git add remote origin GIT_REMOTE_ORIGIN
RUN git clone GIT_BASE_FILES