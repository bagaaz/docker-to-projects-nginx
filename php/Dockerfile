# Seu Dockerfile
FROM php:8.2-fpm

# Instala extensões
RUN docker-php-ext-install pdo_mysql

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y zip unzip

# Instala o Composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

# Instala o Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
RUN apt-get install -y nodejs

# Instala o Python
RUN apt-get install -y python3.11 python3.11-venv

# Cria um ambiente virtual Python e instala o Pip
RUN python3.11 -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"
RUN /opt/venv/bin/python -m ensurepip
RUN /opt/venv/bin/python -m pip install --upgrade pip

WORKDIR /var/www/html