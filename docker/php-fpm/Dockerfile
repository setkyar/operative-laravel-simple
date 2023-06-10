# Use the official PHP 8.2 base image
FROM php:8.2-fpm

# Set the working directory inside the container
WORKDIR /var/www/app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    zip \
    && docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

# Install Composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Copy composer.json and composer.lock to the working directory
COPY composer.json composer.lock ./

# Copy composer.json and composer.lock to the working directory
COPY composer.json composer.lock ./

# Install project dependencies
RUN composer install --no-scripts --no-autoloader

# Copy the application code to the working directory
COPY . .

# Generate the autoload files
RUN composer dump-autoload --no-scripts --optimize

# Set write permissions on the storage and bootstrap/cache directories
RUN chown -R www-data:www-data storage bootstrap/cache

# Set the user to run the container
USER www-data

# Set the entry point for PHP-FPM
CMD ["php-fpm"]
