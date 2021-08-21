FROM httpd:latest

RUN apt update && \
    apt upgrade -y

RUN apt install -y \
    lsb-release \
    ca-certificates \
    apt-transport-https \
    software-properties-common \
    wget \
    gnupg2  

RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/sury-php.list    

RUN wget -qO - https://packages.sury.org/php/apt.gpg | apt-key add -

RUN apt update && \
    apt upgrade -y

RUN apt install -y \
    bash \
    apache2 \
    apache2-bin \
    libapache2-mod-php8.0 \
    curl \
    ca-certificates \
    openssl \
    tzdata \
    openntpd

COPY conf/httpd.conf /usr/local/apache2/conf/httpd.conf
COPY conf/sites-enabled/*.conf /usr/local/apache2/sites-enabled/
# COPY conf/conf-enabled/*.conf /usr/local/apache2/conf-enabled/
