# Start with an official PHP image (with Apache or FPM, depending on your use case)
FROM php:8.2-apache

# Set the working directory in the container
WORKDIR /var/www/html

# Install system dependencies (if needed)
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    zip \
    git \
    && rm -rf /var/lib/apt/lists/*

# Install necessary PHP extensions (add as needed)
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql zip

# Enable Apache mod_rewrite (if using Apache)
RUN a2enmod rewrite

# Copy custom PHP.ini settings (if you have any specific settings)
COPY php.ini /usr/local/etc/php/

# Optionally, copy your application code into the container
# COPY . /var/www/html/

# Expose port 80 for HTTP access
EXPOSE 80

# Start Apache in the foreground
CMD ["apache2-foreground"]
