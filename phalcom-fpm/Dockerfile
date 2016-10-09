FROM php:7.0-fpm
RUN apt-get update && apt-get install -y \
		gcc make autoconf libc-dev pkg-config git \
        openssl \
        libpcre3-dev \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng12-dev \
        zlib1g-dev \
		libmemcached-dev \
	&& docker-php-ext-install -j$(nproc) iconv mcrypt \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include --with-jpeg-dir=/usr/include \
	&& docker-php-ext-install -j$(nproc) gd

RUN git clone https://github.com/php-memcached-dev/php-memcached \ 
    && cd php-memcached \
    && git checkout php7 \
    && phpize \
    && ./configure --disable-memcached-sasl \
    && make && make install \
    && docker-php-ext-enable memcached \
    && cd .. && rm -rf php-memcached

 
# install phalcon
RUN git clone git://github.com/phalcon/cphalcon.git \
    && cd cphalcon/build && bash ./install && cd ../.. && rm -rf cphalcon \
    && docker-php-ext-enable phalcon
