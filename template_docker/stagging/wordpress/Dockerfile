FROM ubuntu:bionic
LABEL maintainer="aryrz stagging - wordpress"
RUN apt-get update
RUN apt-get install -y nginx php-fpm php-mysql systemd
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
RUN sed -i -e "s/;\?daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.2/fpm/php-fpm.conf
RUN echo "\nclear_env = no" >> /etc/php/7.2/fpm/pool.d/www.conf
#COPY FILE
COPY . /var/www/html/
# Nginx config
RUN rm /etc/nginx/sites-enabled/default
ADD ./wordpress.conf /etc/nginx/sites-available/
RUN ln -s /etc/nginx/sites-available/wordpress.conf /etc/nginx/sites-enabled/wordpress.conf

RUN echo "exit 0" > /usr/sbin/policy-rc.d

# Expose ports.
EXPOSE 80
# RUN PHP and NGINX
CMD /etc/init.d/php7.2-fpm start && nginx
