# base image
FROM ubuntu

# MAINTAINER
LABEL maintainer="bikai_xidian@163.com"

# global params
ENV SOURCES_LIST aliyun.sources.list
ENV NGINX_VERSION 1.15.6

# upload and unpack nginx
ADD nginx-${NGINX_VERSION}.tar.gz /starlab/packages

# update apt source list
RUN mv /etc/apt/sources.list /etc/apt/sources.list.backup
ADD ${SOURCES_LIST} /etc/apt
RUN mv /etc/apt/${SOURCES_LIST} /etc/apt/sources.list
RUN apt-get update

# running required command
RUN apt-get install -y build-essential libpcre3-dev zlib1g-dev openssl libssl-dev 
RUN groupadd www
RUN useradd -g www -M -d /starlab/www -s /usr/sbin/nologin www

# mount a dir to container
# ONBUILD VOLUME ["/data"]

# change dir
WORKDIR /starlab/packages/nginx-${NGINX_VERSION}

# execute command to compile nginx
RUN ./configure --user=www --group=www --prefix=/starlab/server/nginx-${NGINX_VERSION} --with-http_stub_status_module --without-http-cache --with-http_ssl_module --with-http_gzip_static_module && make && make install

# add environmental variable
ENV PATH /starlab/server/nginx-${NGINX_VERSION}/sbin:$PATH

#http
EXPOSE 80
#https
EXPOSE 443

# start nginx service
# CMD /bin/sh -c 'nginx -g "daemon off;"'
ENTRYPOINT ["nginx"]
CMD ["-g","daemon off;"]
