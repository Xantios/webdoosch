FROM alpine:3.7 

RUN apk update && apk upgrade &&\
    apk add php7-fpm php7-pdo php7-pdo_mysql nodejs curl git

RUN sed -e 's/127.0.0.1:9000/9000/' \ 
        -e '/allowed_clients/d' \
        -e '/catch_workers_output/s/^;//' \
        -e '/error_log/d' \
        -i /etc/php7/php-fpm.d/www.conf

RUN echo "php_admin_value[sendmail_path] = /usr/sbin/sendmail -S mail:1025 -t" >> /etc/php7/php-fpm.d/www.conf

EXPOSE 9000

ENTRYPOINT /usr/sbin/php-fpm7 --nodaemonize
