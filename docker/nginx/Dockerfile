FROM ubuntu:latest

RUN apt-get update && apt-get install -y -q nginx

COPY default.conf /etc/nginx/conf.d/default.conf

VOLUME ./docker/nginx/default.conf:/etc/nginx/conf.d/default.conf

VOLUME .:/var/www/src

EXPOSE 80

CMD ["nginx","-g","daemon off;"]