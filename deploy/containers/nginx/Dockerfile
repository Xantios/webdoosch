# Currently 3.8 aint ready for primetime yet
FROM alpine:3.7 

# Just get Nginx up and running
RUN apk update && apk upgrade && apk add nginx

# Config nginx
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./nginx.vhost.conf /etc/nginx/conf.d/default.conf

 # Config nginx log to stdout
 RUN ln -sf /dev/stdout /var/log/nginx/access.log \ 
 && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80

CMD /usr/sbin/nginx -g "daemon off;"