FROM php:8.0.0-fpm-alpine
RUN apk add --no-cache mysql-client msmtp perl wget procps shadow libzip libpng libjpeg-turbo libwebp freetype icu

RUN apk add --no-cache --virtual build-essentials \
    icu-dev icu-libs zlib-dev g++ make automake autoconf libzip-dev \
    libpng-dev libwebp-dev libjpeg-turbo-dev freetype-dev && \
    docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp && \
    docker-php-ext-install gd && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install intl && \
    docker-php-ext-install opcache && \
    docker-php-ext-install exif && \
    docker-php-ext-install zip && \
    apk del build-essentials && rm -rf /usr/src/php*

RUN apk add --no-cache unit-openrc unit-php8

RUN wget https://getcomposer.org/composer-stable.phar -O /usr/local/bin/composer && chmod +x /usr/local/bin/composer

# RUN mkdir /var/www/ && groupadd -r www-data && useradd --no-log-init -r -g www-data www-data && \
#     chown -R www-data:www-data /var/www/

#RUN pecl install redis-5.3.4 \
#    && docker-php-ext-enable redis

#RUN ln -sf /dev/stdout /var/log/unit.log

#COPY wordpress /var/www
#RUN chown -R www-data:www-data /var/www/
#COPY config.json /docker-entrypoint.d/.unit.conf.json
#CMD ["unitd", "--no-daemon", "--control", "unix:/var/run/control.unit.sock"]
