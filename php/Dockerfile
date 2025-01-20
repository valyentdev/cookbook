# Use the official PHP Apache image
FROM php:8.4.3-apache

# Copy the application files to the web server's document root
COPY . /var/www/html/

# Set appropriate permissions for the document root
RUN chown -R www-data:www-data /var/www/html

# Expose port 80
EXPOSE 80
