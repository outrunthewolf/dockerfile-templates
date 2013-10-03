# Dockerfile Templates #

Dockerfiles for various stacks, and builds

## Apache2, PHP, Composer ##

A base Dockerfile running, I use these base Dockerfiles as templates for the various stacks I work with

* Apache2
* PHP5
* Composer

## Installation and running ##
Clone the repository, and inside the correct folder run:

```
sudo docker build -t="base/apache2"
```
To build the container, you can name the container anything you want, i've chosen base/apache2

Run the container as a daemon
```
sudo docker run -d base/apache2
```

To see the container, and the public to private port listing you can run:
```
sudo docker ps
```