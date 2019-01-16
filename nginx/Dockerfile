# base image
FROM ubuntu

# MAINTAINER
LABEL maintainer="bikai_xidian@163.com"

# upload and unpack nginx
ADD nginx-1.15.6.tar.gz /starlab/packages

# running required command
RUN rm /etc/apt/sources.list
ADD sources.list /etc/apt
RUN apt-get update
RUN apt-get install -y build-essential libpcre3-dev zlib1g-dev openssl libssl-dev 
RUN groupadd www
RUN useradd -g www -M -d /starlab/www -s /usr/sbin/nologin www

# change dir
WORKDIR /starlab/packages/nginx-1.15.6

# execute command to compile nginx
RUN ./configure --user=www --group=www --prefix=/starlab/server/nginx-1.15.6 --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_gzip_static_module && make && make install

EXPOSE 80
