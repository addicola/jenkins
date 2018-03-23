FROM evarga/jenkins-slave

# Update 
RUN sudo apt-get update
RUN sudo apt-get install python-software-properties software-properties-common
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php

# Install PHP7
RUN sudo apt-get install php7.0 php7.0-fpm php7.0-mysql -y
RUN sudo apt-get --purge autoremove -y

# Install COMPOSER
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod +x composer.phar
RUN mv composer.phar /usr/local/bin/composer

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]