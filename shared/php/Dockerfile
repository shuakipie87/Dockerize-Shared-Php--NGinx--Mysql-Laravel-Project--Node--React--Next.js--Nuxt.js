FROM php:8.3-fpm

# Install PHP extensions and Node/npm
RUN apt-get update && apt-get install -y \
    git curl libpng-dev libonig-dev libxml2-dev zip unzip nodejs npm \
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www
EXPOSE 9000
CMD ["php-fpm"]
