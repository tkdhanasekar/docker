```
$ mkdir apache_docker
```
```
$ cd apache_docker
```

create the docker file
```
$ sudo vim Dockerfile
```
```
FROM ubuntu
MAINTAINER tkdana@gmail.com
ENV TZ=Asia/Kolkata \
DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y
RUN apt-get install tzdata
RUN apt-get install -y apache2
RUN mkdir -p /var/lock/apache2
RUN mkdir -p /var/run/apache2
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV LANG C
COPY index.html /var/www/html/
CMD ["/usr/sbin/apache2","-D","FOREGROUND"]
EXPOSE 80
:wq! save and exit
```
create a html file in the same dir apache_docker
```
$ sudo vim index.html
```
```
<!DOCTYPE html>
<html>
<body>
<h1> DOCKER <h1>
<h1> K8S <h1>
<h1> DEVOPS <h1>
</body>
</html>
:wq! save and exit
```
```
docker build -t myapache .
```
```
docker run -d --name apache_demo -p 8089:80 myapache
```
check with
```
docker ps -a
```
access with http://server_ip:8089

To login to the container
```
docker exec -it name_of_container /bin/bash
```
or
```
docker run --name myapache --rm -i -t myapache bash
```

