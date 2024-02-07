FROM php:8.2-apache

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

RUN  apt-get update 
RUN apt-get install -y --no-install-recommends locales apt-utils git libicu-dev g++ libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev unzip vim nano coreutils g++ 

RUN  echo "en_US.UTF-8 UTF-8" > /etc/locale.gen  \
    &&  echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen \
    &&  locale-gen 

#Install gestionnaire de paquets Composer/Node
RUN curl -sS https://getcomposer.org/installer | php -- \
    && mv composer.phar /usr/local/bin/composer 

RUN curl -sL https://deb.nodesource.com/setup_18.x | bash \
    && apt-get install nodejs -y 

RUN docker-php-ext-configure intl

RUN docker-php-ext-install pdo pdo_mysql mysqli opcache gd intl zip calendar dom mbstring xsl 

RUN pecl install apcu && docker-php-ext-enable apcu 

#Symfony CLI
RUN curl -sS https://get.symfony.com/cli/installer | bash \
    && mv /root/.symfony5/bin/symfony /usr/local/bin/symfony


WORKDIR /var/www/

# Exposer le port 80 pour Apache
EXPOSE 80

# CMD pour démarrer Apache lors de l'exécution du conteneur
CMD ["apache2-foreground"]