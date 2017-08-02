FROM qktong/centos

MAINTAINER qktong <qktong@qq.com>

ENV PHP_VERSION 7.1.7
ENV PHP_MIRROR http://cn2.php.net/get/php-7.1.7.tar.gz/from/this/mirror

RUN CONFIG="\
        --prefix=/usr/local/php \
        --enable-fpm \
        --enable-mysqlnd \
        --with-pdo-mysql \
        --with-mysqli \
        --enable-mbstring \
        --with-curl \
        --enable-sockets \
        --enable-gd-native-ttf \
        --enable-gd-jis-conv \
        --with-openssl \
        --enable-opcache \
    " \
    && groupadd -r www-data \
    && useradd -s /sbin/nologin -g www-data -r www-data \
    && cd /usr/src/ \
    && curl -fSL $PHP_MIRROR -o php.tar.gz \
    && tar -zxvf php.tar.gz \
    && cd php-$PHP_VERSION \
    && ./configure $CONFIG \
    && make && make install \
    && cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf \
    && make clean \
    && rm -rf /usr/local/src/* 

ADD ./php.ini /usr/local/php/lib/
ADD ./www.conf /usr/local/php/etc/php-fpm.d/

EXPOSE 9000

CMD ["/usr/local/php/sbin/php-fpm","-F"]