FROM php:7-fpm
WORKDIR "/application"

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install \
	libmagickwand-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        ghostscript \
        libreoffice \
    && rm -rf /var/lib/apt/lists/*


# New try:
# Already in core: 
# ftp mbstring json session
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions gd imagick mysqli


# Accroding to DockerHub - Installing gd enxtension
#RUN docker-php-ext-configure gd --with-jpeg \
#    && docker-php-ext-install -j$(nproc) gd

#RUN printf "\n" | pecl install imagick & docker-php-ext-enable imagick 

# JSON MSYLI 
#RUN docker-php-ext-install mysqli pdo pdo_mysql json
	
#php5-mysql php5-intl php5-gnupg php5-imagick php5-gd \
#    java-common libreoffice \
#    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* \
