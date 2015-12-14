FROM alpine:3.2
MAINTAINER Akiyoshi Sakaguchi <a-sakaguchi@groovenauts.jp>

ENV NGINX_CONFIG_OPT_ENV --with-http_stub_status_module \
                         --with-http_ssl_module \
                         --with-http_realip_module \
                         --with-http_addition_module \
                         --with-http_sub_module \
                         --with-http_gunzip_module \
                         --with-http_gzip_static_module \
                         --with-http_random_index_module \
                         --with-http_secure_link_module \
                         --prefix=/usr/share/nginx \
                         --sbin-path=/usr/local/sbin/nginx \
                         --conf-path=/etc/nginx/conf/nginx.conf \
                         --pid-path=/var/run/nginx.pid \
                         --http-log-path=/var/log/nginx/access.log \
                         --error-log-path=/var/log/nginx/error.log

RUN apk add --update openssl-dev pcre-dev git \
  && apk add --virtual build-dependencies build-base ruby-dev tar wget bison perl \
  && git clone https://github.com/matsumoto-r/ngx_mruby.git \
  && cd ngx_mruby \
  && sh build.sh \
  && make install \
  && cd / \
  && apk del build-dependencies \
  && rm -rf \
       ngx_mruby \
       /var/cache/apk/*

RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

ONBUILD ADD ngx-mruby/hook /usr/share/nginx/hook
ONBUILD ADD ngx-mruby/conf /etc/nginx/conf

CMD ["nginx", "-g", "daemon off;"]