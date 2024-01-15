FROM php:5.6.40-fpm-alpine

# Install Nginx and OpenRC
RUN apk update && apk add nginx openrc

# Install MariaDB client
RUN apk add mariadb-client

# Install libcurl
RUN apk add curl-dev

# Install mysqli extension
RUN docker-php-ext-install mysqli

# Configure PHP
COPY php/php.ini /usr/local/etc/php/php.ini

# Copy Nginx configuration
COPY nginx/nginx.conf /etc/nginx/nginx.conf

# Copy project files
COPY app/src /var/www/html

# Create directory for nginx tipically used to store the process ID of the running Nginx instance
# Ensure that the Nginx process has proper permissions to write to the /run/nginx directory. 
RUN mkdir -p /run/nginx
RUN chmod -R 777 /var/log
RUN chown -R nginx:nginx /run/nginx

# Start PHP FPM
CMD ["php-fpm"]