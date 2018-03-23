FROM evarga/jenkins-slave


# Install PHP7
RUN sudo LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN sudo apt-get update
RUN sudo apt-get install -y php7.1 php7.1-xdebug php7.1-xsl php7.1-dom \
        php7.1-zip php7.1-mbstring

# Install Update
RUN sudo apt-get update
RUN sudo apt-get -y --purge autoremove
RUN sudo insall -y git unzip

# Install COMPOSER
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
RUN sudo chown -R $USER:$USER ~/.composer/

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]