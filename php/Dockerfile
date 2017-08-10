FROM ubuntu:16.04

MAINTAINER Zoltán Borsos

ENV TERM=linux
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y upgrade \
    && apt-get -y --no-install-recommends install locales apt-utils \
    && locale-gen en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get -y --no-install-recommends install software-properties-common \
    && add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    && apt-get -y --no-install-recommends install php7.2 php7.2-bcmath \
    php7.2-cli php7.2-common php7.2-curl php7.2-fpm php7.2-gd php7.2-imap \
    php7.2-intl php7.2-json php7.2-mbstring php7.2-mysql php7.2-opcache \
    php7.2-soap php7.2-sqlite3 php7.2-xml php7.2-xmlrpc php7.2-zip \
    php-lua php-gearman php-mongo php-libsodium php-mailparse php-amqp \
    php-apcu-bc php-memcached php-redis php-ssh2 php-imagick php-xdebug \
    php-apcu php-pear curl zip unzip git \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && mkdir /run/php \
    && apt-get remove -y --purge software-properties-common \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* ~/.composer

ADD php-fpm.conf /etc/php/7.2/fpm/php-fpm.conf
ADD www.conf /etc/php/7.2/fpm/pool.d/www.conf

EXPOSE 9000

CMD ["php-fpm7.2"]
