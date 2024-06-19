# Use uma imagem oficial do PHP com Apache, versão 8.1
FROM php:8.1-apache

# Instale as dependências do sistema necessárias
RUN apt-get update && apt-get install -y \
    libzip-dev \
    unzip \
    && docker-php-ext-install zip

# Defina o diretório de trabalho
WORKDIR /usr/src/myapp

# Copie o composer.json e composer.lock para o diretório de trabalho
COPY composer.json composer.lock ./

# Instale o Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    rm composer-setup.php

# Defina a variável de ambiente para permitir que o Composer seja executado como superusuário
ENV COMPOSER_ALLOW_SUPERUSER=1

# Instale as dependências do Composer
RUN composer install

# Carregue as dependências do Composer
RUN composer dump-autoload --optimize --classmap-authoritative

# Copie o código do servidor WebSocket
COPY websocket_server.php /usr/src/myapp

# Exponha a porta 8000
EXPOSE 8000

# Inicie o servidor WebSocket quando o contêiner for iniciado
CMD ["php", "websocket_server.php"]