# Utiliser une image PHP officielle avec Apache
FROM php:8.2-apache
# Configuration de l'environnement
ENV APACHE_DOCUMENT_ROOT=/var/www/testApp

# Installation des dépendances nécessaires
RUN apt-get update \
    && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libwebp-dev \
        libonig-dev \
        libzip-dev \
        unzip \
        git \
        curl

# Installation des extensions PHP nécessaires
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl

# Installation de Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Configuration Apache
RUN a2enmod rewrite

# Copie des fichiers de l'application dans le conteneur
COPY . /var/www/testApp

# remplace la configuration de apache
COPY ./Docker/Server.conf /etc/apache2/sites-available/000-default.conf

# Installation des dépendances avec Composer

RUN cd /var/www/testApp && \
    composer install --no-scripts --no-interaction

# Configuration du propriétaire des fichiers
RUN chown -R www-data:www-data /var/www/

# change emplacement curseur commande
WORKDIR /var/www/testApp

#Exposition du port 80
EXPOSE 80

# Commande pour exécuter Apache
CMD ["apache2-foreground"]
