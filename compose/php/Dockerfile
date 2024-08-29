FROM php:8.0-fpm-alpine

# Copy File Config
ADD ./compose/php/www.conf /usr/local/etc/php-fpm.d/www.conf

# ADD and set Group
RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel

# Create folder to run
RUN mkdir -p /var/www/html

# Set Profile
RUN chown laravel:laravel /var/www/html

COPY compose/php/php.ini /usr/local/etc/php/conf.d/

# Work in the specific space
WORKDIR /var/www/html

RUN chown -R laravel:laravel /var/www/html
RUN chmod -R 775 /var/www/html

# Install dependencies
RUN apk add --no-cache \
    freetype \
    libpng \
    libjpeg-turbo \
    freetype-dev \
    libpng-dev \
    libjpeg-turbo-dev

RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
    && docker-php-ext-install gd

RUN NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
    docker-php-ext-install -j${NPROC} gd 

RUN apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

RUN docker-php-ext-install pdo pdo_mysql    
RUN docker-php-ext-install exif

# install and enable xdebug
RUN apk add --no-cache $PHPIZE_DEPS \
	&& pecl install xdebug-3.1.5 \
	&& docker-php-ext-enable xdebug
