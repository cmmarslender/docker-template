FROM johnpbloch/phpfpm:7.0

RUN apt-get update \
	&& apt-get install -y libgearman-dev unzip wget \
	&& apt-get clean \
	&& wget https://github.com/wcgallego/pecl-gearman/archive/master.zip \
	&& unzip master.zip \
	&& rm master.zip \
	&& ( \
		cd pecl-gearman-master \
		&& phpize \
		&& ./configure \
		&& make -j$(nproc) \
		&& make install \
	) \
	&& rm -r pecl-gearman-master \
	&& docker-php-ext-enable gearman

RUN curl -L https://phar.phpunit.de/phpunit.phar > /tmp/phpunit.phar \
    && chmod +x /tmp/phpunit.phar \
    && mv /tmp/phpunit.phar /usr/local/bin/phpunit

RUN apt-get install -y git subversion wget

CMD ["php-fpm"]

EXPOSE 9000
