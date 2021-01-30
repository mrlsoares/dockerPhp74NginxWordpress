FROM php:7.4-fpm-alpine

WORKDIR /var/www/html

RUN apk add --update --no-cache libgd libpng-dev libjpeg-turbo-dev freetype-dev

RUN apk upgrade
RUN apk add --no-cache  --virtual .phpize-deps $PHPIZE_DEPS \
    && apk add --no-cache --virtual .build-deps \
    shadow \
    build-base \
    shadow \
    curl \
    tzdata \
    php7 \
    php7-fpm \
    php7-common \
    php7-pdo \
    php7-pdo_mysql \
    php7-mcrypt \
    php7-mbstring \
    php7-xml \
    php7-openssl \
    php7-json \
    php7-phar \
    php7-zip \
    php7-gd \
    php7-dom \
    php7-session \
    php7-zlib \
    supervisor \
    libxml2-dev \
    php7-soap \
    bash \
    nano

#RUN docker-php-ext-install  mysqli pdo pdo_mysql && docker-php-ext-enable pdo_mysql
RUN docker-php-ext-install -j$(nproc) gd
# Adjust TimeZone
RUN cp  /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
RUN echo "America/Sao_Paulo" > /etc/timezone
RUN rm -rf /var/cache/apk/*
#RUN rm -rf /var/www/html


RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar
RUN mv wp-cli.phar /usr/local/bin/wp

RUN usermod -u 1000 www-data
RUN chown -R www-data:www-data /var/www/html

USER www-data

EXPOSE 9000

ENTRYPOINT ["php-fpm"]