# Dockerfile Templates #

Dockerfiles for various stacks, and builds

## base-nginx ##

* Nginx
* PHP5
* Composer

## base-apache2 ##

* Apache2
* PHP5
* Composer

## Installation and running ##
Clone the repository, and inside the correct folder run:

```
sudo docker build -t base/apache2 .
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