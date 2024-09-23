FROM php:8.0-fpm-alpine

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
# ADD and set Group
RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel

# Set Profile to All Files
RUN chown -R laravel:laravel /var/www/html
RUN docker-php-ext-install exif
RUN docker-php-ext-install gd

# Run in work space
WORKDIR /var/www/html