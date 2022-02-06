ARG PHP_VERSION=8.1

FROM wordpress:php${PHP_VERSION}-fpm-alpine

# Add XDebug
RUN apk --no-cache add autoconf g++ make && pecl install xdebug && docker-php-ext-enable xdebug && rm -rf /tmp/pear; apk del autoconf g++ make;

# Install Wordpress CLI
RUN wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp

# Make sure we have the latest composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install PHPUnit
RUN wget -O phpunit https://phar.phpunit.de/phpunit-9.phar && chmod +x phpunit && mv phpunit /usr/local/bin/phpunit

# Output PHP and Wordpress CLI versions
RUN php -i && wp --allow-root --version && composer --version && phpunit --version
