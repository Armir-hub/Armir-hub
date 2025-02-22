#!/bin/bash
# Update package lists
apt-get update
apt-get upgrade -y

# Install required packages
apt-get install -y apache2 \
                    ghostscript \
                    libapache2-mod-php \
                    mysql-server \
                    php \
                    php-bcmath \
                    php-curl \
                    php-imagick \
                    php-intl \
                    php-json \
                    php-mbstring \
                    php-mysql \
                    php-xml \
                    php-zip \
                    unzip \
                    curl

# Optionally, start Apache and MySQL services
systemctl start apache2
systemctl enable apache2
systemctl start MySQL   
systemctl enable MySQL  

# Download WordPress
curl -O https://wordpress.org/latest.zip

# Unzip WordPress into /var/www/html
unzip latest.zip -d /var/www/html/

# Move WordPress files to /var/www/html
mv /var/www/html/wordpress/* /var/www/html/

# Remove the now-empty wordpress directory and the zip file
rm -rf /var/www/html/wordpress
rm latest.zip

# Set proper permissions
chown -R www-data:www-data /var/www/html
chmod -R 755 /var/www/html

# Remove the default Apache index.html file
rm /var/www/html/index.html
