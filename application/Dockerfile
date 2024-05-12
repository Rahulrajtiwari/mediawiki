# Use the official MediaWiki image as a base
FROM mediawiki:latest

# Set the working directory in the container
WORKDIR /var/www/html

# Install the intl PHP extension
RUN apt-get update && apt-get install -y libicu-dev && docker-php-ext-install intl

# Install mysqli extension
RUN docker-php-ext-install mysqli

# Copy the MediaWiki files into the container
COPY LocalSettings.php /var/www/html/

ADD https://releases.wikimedia.org/mediawiki/1.41/mediawiki-1.41.1.tar.gz /var/www/html/


# Extract the MediaWiki files
RUN tar -xzf /var/www/html/mediawiki-1.41.1.tar.gz
RUN mv /var/www/html/mediawiki-1.41.1/* /var/www/html/ 

# Expose port 80
EXPOSE 80

# Start the web server
CMD ["apache2-foreground"]