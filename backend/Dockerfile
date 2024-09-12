FROM php:fpm-alpine3.20

# Install dependencies
RUN apk update \
  && apk add --no-cache \
  git \
  curl \
  libpng-dev \
  libzip-dev \
  oniguruma-dev \
  zlib-dev \
  postgresql-dev \
  libxml2-dev \
  unzip \
  bzip2-dev \
  gd-dev

# Install PHP extensions
RUN docker-php-ext-install \
  pdo \
  pdo_pgsql \
  pgsql \
  zip \
  bcmath \
  gd

# Set working directory
COPY . /var/www/
WORKDIR /var/www/

# Set permissions
RUN chown -R www-data:www-data /var/www \
  && chmod -R 775 /var/www/storage

# Copy Composer from the Composer image
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Install Composer dependencies
COPY composer.json ./
RUN composer install


CMD ["php-fpm"]
