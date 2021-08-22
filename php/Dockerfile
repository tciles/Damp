FROM php:8-fpm

RUN apt update && \
    apt upgrade -y

RUN apt install -y \
    wget \
    git \
    libicu-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev

RUN docker-php-ext-configure gd --with-freetype --with-jpeg

# Possible values for ext-name:
#   bcmath bz2 calendar ctype curl dba dom enchant exif ffi fileinfo filter ftp gd gettext gmp hash iconv imap intl json
#   ldap mbstring mysqli oci8 odbc opcache pcntl pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite
#   pgsql phar posix pspell readline reflection session shmop simplexml snmp soap sockets sodium spl standard sysvmsg
#   sysvsem sysvshm tidy tokenizer xml xmlreader xmlwriter xsl zend_test zip
RUN docker-php-ext-install -j$(nproc) intl opcache gd pdo_mysql zip

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

RUN usermod -u 1000 www-data
RUN chown -R www-data:www-data /var/www

# Symfony
RUN wget https://get.symfony.com/cli/installer -O - | bash    
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony
RUN symfony check:requirements

# Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN mv composer.phar /usr/local/bin/composer
RUN php -r "unlink('composer-setup.php');"

COPY "./conf.d/*" "$PHP_INI_DIR/conf.d/"
