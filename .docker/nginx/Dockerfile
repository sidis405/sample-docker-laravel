FROM nginx:1.12
LABEL maintainer="Sidrit Trandafili"

RUN rm /etc/nginx/conf.d/default.conf

COPY .docker/nginx/nginx.conf /etc/nginx/nginx.conf
COPY .docker/nginx/conf.d/*.conf /etc/nginx/conf.d/
COPY public/ /var/www/html/public
