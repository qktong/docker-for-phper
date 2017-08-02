FROM qktong/centos

MAINTAINER qktong <qktong@qq.com>

ENV NGINX_VERSION 1.11.10

RUN CONFIG="\
        --prefix=/usr/local/nginx \
        --user=nginx \
        --group=nginx \
        --with-http_ssl_module \
        --with-http_realip_module \
        --with-http_addition_module \
        --with-http_sub_module \
        --with-http_dav_module \
        --with-http_flv_module \
        --with-http_mp4_module \
        --with-http_gunzip_module \
        --with-http_gzip_static_module \
        --with-http_random_index_module \
        --with-http_secure_link_module \
        --with-http_stub_status_module \
        --with-http_auth_request_module \
        --with-http_xslt_module=dynamic \
        --with-http_image_filter_module=dynamic \
        --with-http_geoip_module=dynamic \
        --with-http_perl_module=dynamic \
        --with-threads \
        --with-stream \
        --with-stream_ssl_module \
        --with-stream_ssl_preread_module \
        --with-stream_realip_module \
        --with-stream_geoip_module=dynamic \
        --with-http_slice_module \
        --with-mail \
        --with-mail_ssl_module \
        --with-compat \
        --with-file-aio \
        --with-http_v2_module \
    " \
    && groupadd -r nginx \
    && useradd -s /sbin/nologin -g nginx -r nginx \
    && cd /usr/src/ \
    && curl -fSL http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz -o nginx.tar.gz \
    && tar -zxvf nginx.tar.gz \
    && cd nginx-$NGINX_VERSION \
    && ./configure $CONFIG \
    && make && make install \
    && make clean \
    && rm -rf /usr/local/src/* \
    && ln -s /usr/local/nginx/sbin/nginx /usr/bin/nginx 

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]