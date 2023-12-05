# Install composer dependencies first
FROM php:8.2-alpine as vendor
WORKDIR /var/www
COPY --from=composer/composer:2-bin /composer /usr/local/bin/composer
COPY composer.json /var/www/composer.json
RUN composer install --prefer-dist --no-dev --optimize-autoloader --no-scripts

FROM php:8.2-alpine
WORKDIR /var/www
COPY src /var/www/src
COPY php-cs-fixer /var/www/php-cs-fixer
# Only take the dependencies (not composer itself) into the container
COPY --from=vendor /var/www/vendor /var/www/vendor
ENTRYPOINT ["/var/www/php-cs-fixer"]
