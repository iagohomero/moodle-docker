# Use the official PHP with Apache image (PHP 8.1)
FROM php:8.1-apache

# Update packages and install required dependencies
RUN apt-get update && apt-get install -y \
    wget unzip rsync netcat-traditional curl \
    libicu-dev libpq-dev libjpeg-dev libfreetype6-dev \
    libldap2-dev libpng-dev libxslt-dev unzip zip nano cron \
    libzip-dev pkg-config \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure zip \
    && docker-php-ext-install -j$(nproc) mysqli gd intl ldap pdo_mysql soap zip bcmath opcache sockets exif

# Copy the custom php.ini file to PHP configuration directory
COPY .docker/php/php.ini /usr/local/etc/php/conf.d/

# Install necessary PHP extensions for Moodle
RUN pecl install apcu redis \
    && docker-php-ext-enable apcu redis

# Set the working directory to the web root
WORKDIR /var/www/html

# Download the latest Moodle version and extract it
RUN wget https://download.moodle.org/download.php/direct/stable405/moodle-latest-405.tgz \
    && tar -zxvf moodle-latest-405.tgz --strip-components=1 -C /var/www/html \
    && rm moodle-latest-405.tgz \
    && chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

# Create the Moodle data directory and set appropriate permissions
RUN mkdir -p /var/www/moodledata \
    && chown -R www-data:www-data /var/www/moodledata \
    && chmod -R 770 /var/www/moodledata

# Configure cron job for Moodle
RUN echo "*/1 * * * * www-data php -q /var/www/html/admin/cli/cron.php > /var/log/moodle_cron.log 2>&1" >> /etc/crontab

# Expose the default Apache port
EXPOSE 80

# Start Apache and cron service together
CMD service cron start && apache2-foreground
