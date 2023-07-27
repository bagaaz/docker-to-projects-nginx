# Seu Dockerfile
FROM php:8.2-fpm

ARG UID=1000
ARG GID=1000

RUN groupadd -g $GID devuser
RUN useradd -m -u $UID -g $GID devuser

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

RUN find /var/www -type d -exec chmod 0755 {} \;
RUN find /var/www -type f -exec chmod 0644 {} \;
RUN chown -Rf www-data:www-data /var/www/html
RUN chown -Rf www-data:www-data /var/www/html

USER devuser

WORKDIR /var/www/html

EXPOSE 9000 3000