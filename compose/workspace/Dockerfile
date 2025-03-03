FROM php:8.0-fpm-alpine

COPY ./compose/workspace/run.sh /tmp

WORKDIR /var/www/html

RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 775 /var/www/html

ENTRYPOINT ["/tmp/run.sh"]