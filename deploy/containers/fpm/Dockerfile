FROM alpine:3.7 

# Copy in hooks
COPY hooks/PreStart /prestart.sh
COPY hooks/Main /main.sh

# Run APK to get repo up2date
# Install some usefull tools
# Install PHP components
RUN apk update && apk upgrade &&\
    apk add nodejs curl git &&\ 
    apk add php7-fpm php7-cli php7-pdo php7-pdo_mysql php7-mbstring php7-json php7-session php7-ctype php7-tokenizer php7-phar php7-dom php7-xml php7-xmlwriter php7-simplexml

# Install composer
RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

# Educate FPM a bit 
RUN sed -e 's/127.0.0.1:9000/9000/' \ 
        -e '/allowed_clients/d' \
        -e '/catch_workers_output/s/^;//' \
        -e '/error_log/d' \
        -i /etc/php7/php-fpm.d/www.conf

# Use the included mailer 
RUN echo "php_admin_value[sendmail_path] = /usr/sbin/sendmail -S mail:1025 -t" >> /etc/php7/php-fpm.d/www.conf

#EXPOSE 9000 # Enable if you need it

# sleep 1 because storage needs sync stime
# https://github.com/moby/moby/issues/9547
RUN echo "Running FPM Prestart Hook " ; chmod +x /prestart.sh ; sleep 1; /prestart.sh
RUN echo "Running Start Hook " ; chmod +x /main.sh

WORKDIR /var/www/

ENTRYPOINT /main.sh
