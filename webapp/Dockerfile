# Use uma imagem oficial do PHP com Apache
FROM php:7.4-apache

# Instale as dependências do sistema necessárias
RUN apt-get update && apt-get install -y \
    libzip-dev \
    unzip \
    && docker-php-ext-install zip

# Habilitar módulos Apache necessários
RUN a2enmod rewrite

# Defina o diretório de trabalho
WORKDIR /var/www/html

# Copie o composer.json e composer.lock para o diretório de trabalho
COPY composer.json composer.lock ./

# Instale o Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    rm composer-setup.php

# Instale as dependências do Composer
RUN composer install --no-dev --no-scripts --no-autoloader

# Carregue as dependências do Composer
RUN composer dump-autoload --optimize --classmap-authoritative

# Copie os arquivos da aplicação para o diretório /var/www/html no contêiner
COPY public_html/ /var/www/html
COPY .env /var/www/html

# Exponha a porta 80
EXPOSE 80

# Inicie o Apache quando o contêiner for iniciado
CMD ["apache2-foreground"]