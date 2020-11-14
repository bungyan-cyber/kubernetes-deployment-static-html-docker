FROM ubuntu:latest

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install apache2 -y
RUN rm -rf /var/www/html/index.html
COPY . /var/www/html/

CMD apachectl -DFOREGROUND

