FROM php:8.2-apache
WORKDIR /var/www/html

# Mod Rewrite
RUN a2enmod rewrite

ENV APACHE_DOCUMENT_ROOT /var/www/html/public

# Apache Document Root
RUN sed -ri -e "s!/var/www/html!$APACHE_DOCUMENT_ROOT!g" /etc/apache2/sites-available/*.conf

# Modify php.ini configuration
RUN sed -ri -e "s!post_max_size = 8M!post_max_size = 10M!g"  /usr/local/etc/php/*.ini-development
RUN sed -ri -e "s!post_max_size = 8M!post_max_size = 10M!g"  /usr/local/etc/php/*.ini-production

RUN sed -ri -e "s!upload_max_filesize = 2M!upload_max_filesize = 10M!g"  /usr/local/etc/php/*.ini-development
RUN sed -ri -e "s!upload_max_filesize = 2M!upload_max_filesize = 10M!g"  /usr/local/etc/php/*.ini-production

RUN sed -ri -e "s!max_file_uploads = 150!max_file_uploads = 150!g"  /usr/local/etc/php/*.ini-development
RUN sed -ri -e "s!max_file_uploads = 150!max_file_uploads = 150!g"  /usr/local/etc/php/*.ini-production


# RUN sed -i "s!post_max_size=10M!g" /usr/local/etc/php/*.ini-development
# RUN sed -i "s!post_max_size=10M!g" /usr/local/etc/php/*.ini-production

# Linux Library
RUN apt-get update -y && apt-get install -y \
    libicu-dev \
    libpq-dev \
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

# PHP Extensions
RUN docker-php-ext-install zip gettext intl gd
RUN docker-php-ext-install bcmath

# Add PDO Extensions
RUN docker-php-ext-install pdo_mysql pdo_pgsql

RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

# Install system dependencies and Node.js
RUN apt-get update && apt-get install -y \
    curl \
    && curl -sL https://deb.nodesource.com/setup_16.x | bash - \
    && apt-get install -y nodejs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*



# Add Permission For Laravel Logs (Can be deleted, as the permission is in makefile)
RUN chmod -R 755 /var/www/html
RUN chown -R www-data:www-data /var/www/html

RUN chmod -R ugo+rw /var/www/html/ || chmod 775 -R /var/www/html/