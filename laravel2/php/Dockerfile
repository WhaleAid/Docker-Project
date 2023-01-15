FROM php:7.4-fpm

# Copy
COPY ./laravel2 .

# Install Composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN apt-get update

# Get Node
RUN curl -sL https://deb.nodesource.com/setup_lts.x | bash -

# Installs
RUN apt-get install -y \
    libzip-dev \
    nodejs \
    zip

# Extensions
RUN docker-php-ext-install mysqli pdo pdo_mysql zip

# Start
RUN composer install
RUN npm i
RUN chmod -R 777 /var/www/html/public
RUN chmod -R 777 /var/www/html/storage
RUN npm run build
RUN php artisan key:generate 
RUN php artisan migrate:fresh --seed