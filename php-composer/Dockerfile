# Use a PHP 8.2 base image
FROM php:8.2-fpm

ARG COMPOSER_PKG_NAME
ARG COMPOSER_PKG_AUTHOR
ARG COMPOSER_PKG_TYPE
ARG COMPOSER_PKG_LICENSE

# Set the working directory
WORKDIR /var/www/html

# Copy the application code to the working directory
COPY . /var/www/html

# Install dependencies using Composer
RUN apt-get update && \
    apt-get install -y \
        zip \
        unzip \
        git \
    && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install PHP extensions
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Install NGINX webserver
RUN apt-get install -y nginx

# Configure NGINX
COPY nginx-config.conf /etc/nginx/sites-available/default

# Initialize Composer
RUN composer init --name '${COMPOSER_PKG_NAME}' --author '${COMPOSER_PKG_AUTHOR}' --type '${COMPOSER_PKG_AUTHOR}' --license '${COMPOSER_PKG_LICENSE}'

# Run Composer to install project dependencies
RUN composer install --no-ansi --no-dev --no-interaction --no-progress --optimize-autoloader

# Expose port 80 for the NGINX server
EXPOSE 80

# Start both NGINX and PHP-FPM servers
CMD service nginx start && php-fpm
