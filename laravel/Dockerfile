FROM php:8-apache
WORKDIR /var/www/html

# Mod Rewrite
RUN a2enmod rewrite

ENV APACHE_DOCUMENT_ROOT /var/www/html/public

# Apache Document Root
RUN sed -ri -e "s!/var/www/html!$APACHE_DOCUMENT_ROOT!g" /etc/apache2/sites-available/*.conf

# Linux Library
RUN apt-get update -y && apt-get install -y \
    libicu-dev \
    libmariadb-dev \
    unzip zip \
    zlib1g-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libxml2-dev \
    libzip-dev


# Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# PHP Extension, Add as needed by your project
RUN docker-php-ext-install zip gettext intl pdo_mysql gd

RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

# Add Permission For Laravel Logs (Can be deleted, as the permission is in makefile)
RUN chmod -R 755 /var/www/html
RUN chown -R www-data:www-data /var/www/html

RUN chmod -R ugo+rw /var/www/html/ || chmod 775 -R /var/www/html/
