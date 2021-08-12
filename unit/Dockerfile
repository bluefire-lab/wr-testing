FROM nginx/unit:1.24.0-php8.0

# Install required packages OS/PHP
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    less \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysqli pdo pdo_mysql

# Enable Redis
RUN pecl install redis-5.3.4 \
    && docker-php-ext-enable redis

# Install composer
RUN curl -o /usr/local/bin/composer https://getcomposer.org/composer-stable.phar && chmod +x /usr/local/bin/composer

# Install wpcli
RUN curl -o /bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod 755 /bin/wp
# RUN curl -o /bin/wp-cli.phar https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
# COPY wp-su.sh /bin/wp
# RUN chmod +x /bin/wp-cli.phar

# Output logs to stdout
RUN ln -sf /dev/stdout /var/log/unit.log

# Copy PHP custom ini files
RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini
COPY php /usr/local/etc/php/conf.d

COPY wordpress /var/www
RUN chown -R www-data:www-data /var/www/
WORKDIR /var/www

COPY config.json /docker-entrypoint.d/.unit.conf.json
CMD ["unitd", "--no-daemon", "--control", "unix:/var/run/control.unit.sock"]
