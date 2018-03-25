FROM evarga/jenkins-slave

# Install Update
RUN sudo apt-get update
RUN sudo apt-get -y --purge autoremove

# Common
RUN apt-get update \
	&& apt-get install -y python-setuptools \ 
		curl \
		git \
		nano \
		sudo \
		unzip \
		openssh-server \
		openssl \
		supervisor \
		nginx \
		memcached \
		ssmtp \
		cron 

RUN apt-get update && \
	apt-get install -y --no-install-recommends apt-utils \ 
		software-properties-common \
		python-software-properties \
		language-pack-en-base

# Install PHP7
RUN sudo LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN sudo apt-get update
RUN apt-get install -y php7.1-fpm \
		php7.1-mysql \
	    php7.1-curl \
	    php7.1-gd \
	    php7.1-intl \
	    php7.1-mcrypt \
	    php-memcache \
	    php7.1-sqlite \
	    php7.1-tidy \
	    php7.1-xmlrpc \
	    php7.1-pgsql \
	    php7.1-ldap \
	    freetds-common \
	    php7.1-pgsql \
	    php7.1-sqlite3 \
	    php7.1-json \
	    php7.1-xml \
	    php7.1-mbstring \
	    php7.1-soap \
	    php7.1-zip \
	    php7.1-cli \
	    php7.1-sybase \
	    php7.1-odbc

# Cleanup
RUN apt-get remove --purge -y software-properties-common \
	python-software-properties && \
	apt-get autoremove -y && \
	apt-get clean && \
	apt-get autoclean

# Install COMPOSER
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
RUN sudo chown -R $USER:$USER ~/.composer/

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]