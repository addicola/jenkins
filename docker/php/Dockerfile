FROM evarga/jenkins-slave


# Install PHP7
RUN sudo LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN sudo apt-get update
RUN sudo apt-get install -y php7.1 php7.1-xdebug php7.1-xsl php7.1-dom \
        php7.1-zip php7.1-mbstring

# Install Update
RUN sudo apt-get update
RUN sudo apt-get -y --purge autoremove

# Common
RUN apt-get update \
	&& apt-get install -y \
		openssl \
		git

# PHP
# xml
RUN apt-get update \
	&& apt-get install -y \
	libxml2-dev \
	libxslt-dev \
	&& docker-php-ext-install \
		dom \
		xmlrpc \
		xsl

# images
RUN apt-get update \
	&& apt-get install -y \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng12-dev \
	libgd-dev \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install \
		gd \
		exif

# database
RUN docker-php-ext-install \
	mysqli \
	pdo \
	pdo_mysql

# mcrypt
RUN apt-get update \
	&& apt-get install -y libmcrypt-dev \
	&& docker-php-ext-install mcrypt

# strings
RUN docker-php-ext-install \
	gettext \
	mbstring

# Install COMPOSER
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
RUN sudo chown -R $USER:$USER ~/.composer/

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]