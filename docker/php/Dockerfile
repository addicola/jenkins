FROM evarga/jenkins-slave


# Install PHP7
RUN sudo LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN sudo apt-get update
RUN sudo apt-get install -y php7.1 php7.1-xdebug php7.1-xsl php7.1-dom \
        php7.1-zip php7.1-mbstring

# Install Update
RUN sudo apt-get update
RUN sudo apt-get -y --purge autoremove
RUN sudo apt-get install -y git unzip

# Install Docker ext 
RUN apt-get install libldap2-dev -y && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install ldap
RUN sudo apt-get install -y docker-php-ext-install docker-php-ext-install mbstring \
        && docker-php-ext-install curl \
        && docker-php-ext-install mysqli \
	&& docker-php-ext-install pcntl \
	&& docker-php-ext-install pdo \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install phar \
	&& docker-php-ext-install posix \
	&& docker-php-ext-install simplexml \
	&& docker-php-ext-install soap 

# Install COMPOSER
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
RUN sudo chown -R $USER:$USER ~/.composer/

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]