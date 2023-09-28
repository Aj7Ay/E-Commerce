# Build stage for Composer
FROM composer:2.3.8 as composer_build

WORKDIR /app
COPY . /app
RUN composer install --optimize-autoloader --no-dev --ignore-platform-reqs --no-interaction --no-plugins --no-scripts --prefer-dist

# Final image
FROM php:8.1.8

# Copy the application files from the composer_build stage
COPY --from=composer_build /app/ /app/

WORKDIR /app

# Expose port 9000 within the container
EXPOSE 9000

# Start the Laravel application on port 9000
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=9000"]
