# Use a PHP 8 base image
FROM php:8.0-apache

# Set the working directory
WORKDIR /var/www/html

# Copy the application code to the working directory
COPY . /var/www/html

# Install dependencies using Composer
RUN apt-get update && \
    apt-get install -y \
        git \
        zip \
        unzip && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install PHP extensions and enable Apache rewrite module
RUN docker-php-ext-install mysqli pdo pdo_mysql && \
    a2enmod rewrite

# Run Composer to install project dependencies
RUN composer install

# Expose port 80 for the Apache server
EXPOSE 80

# Start the Apache server
CMD ["apache2-foreground"]
