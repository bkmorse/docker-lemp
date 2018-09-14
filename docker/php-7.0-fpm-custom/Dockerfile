FROM php:7.1-fpm-stretch

# Install modules
RUN apt-get update && apt-get install -y \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libmcrypt-dev \
	libpng-dev \
	curl \
	vim

RUN rm /etc/apt/preferences.d/no-debian-php && \
	apt-get update && apt-get install -y libxml2-dev php-soap && docker-php-ext-install soap

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install gd

RUN docker-php-ext-install mcrypt

RUN docker-php-ext-install mysqli

RUN docker-php-ext-install zip

RUN docker-php-ext-install pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php && \
	chmod +x composer.phar && \
	mv composer.phar /usr/local/bin/composer

# setup paths
RUN echo "" >> ~/.bashrc && \
	export COMPOSER_ALLOW_SUPERUSER=1 && \
	echo 'export PATH="~/.composer/vendor/bin:$PATH"' >> ~/.bashrc

RUN pecl install --onlyreqdeps --force redis \
	&& rm -rf /tmp/pear \
	&& docker-php-ext-enable redis

COPY php.ini /usr/local/etc/php/

CMD ["php-fpm"]