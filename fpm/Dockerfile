FROM php:5.6-fpm

ADD debian8.sources /etc/apt/sources.list
# extions

# Install Core extension
#
#bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd #gettext gmp hash iconv 
#imap interbase intl json ldap mbstring mcrypt mssql mysql mysqli oci8 odbc #opcache pcntl 
#pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite #pgsql phar posix 
#pspell readline recode reflection session shmop simplexml snmp soap sockets #spl standard 
#sybase_ct sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc #xmlwriter xsl zip
#
# Must install dependencies for your extensions manually, if need.
RUN apt-get update && apt-get install -y \
        apt-utils \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \

    # no dependency extension
    && docker-php-ext-install gettext mysqli opcache pdo_mysql sockets

# Install PECL extensions
RUN apt-get install -y \



    # for memcached
    libmemcached-dev \

    && pecl install memcache && docker-php-ext-enable memcache \
    && pecl install memcached && docker-php-ext-enable memcached \
    && pecl install gearman && docker-php-ext-enable gearman \


    && pecl install xdebug && docker-php-ext-enable xdebug \
    && pecl install redis && docker-php-ext-enable redis \
    && pecl install xhprof && docker-php-ext-enable xhprof \

    && docker-php-source delete \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* \
    && echo 'PHP 5.6 installed.'

# Other extensions
# RUN curl -fsSL 'https://xcache.lighttpd.net/pub/Releases/3.2.0/xcache-3.2.0.tar.gz' -o xcache.tar.gz \
#     && mkdir -p xcache \
#     && tar -xf xcache.tar.gz -C xcache --strip-components=1 \
#     && rm xcache.tar.gz \
#     && ( \
#         cd xcache \
#         && phpize \
#         && ./configure --enable-xcache \
#         && make -j$(nproc) \
#         && make install \
#     ) \
#     && rm -r xcache \
#     && docker-php-ext-enable xcache

    # open pid file
#RUN sed -i '/^;pid\s*=\s*/s/\;//g' /usr/local/etc/php-fpm.d/www.conf \

    # add php-fpm to service
   # && cp services/php/5.6/php-fpm /etc/init.d/php-fpm && chmod +x /etc/init.d/php-fpm
    # && chkconfig --add php-fpm

# ADD data/packages/php-tools/composer.phar /usr/local/bin/composer
# RUN chmod 755 /usr/local/bin/composer

#xdebug
#ADD ./xdebug-2.5.4.tgz /root/xdebug-2.5.4.tgz && pecl install /root/xdebug-2.5.4.tgz

RUN pecl install https://pecl.php.net/get/xdebug-2.5.4.tgz
RUN docker-php-ext-enable xdebug

#WORKDIR "/var/www"

################################################################################
# Volumes
################################################################################

#VOLUME ["/var/www"]

# extends from parent
# EXPOSE 9000
# CMD ["php-fpm"]
# 解决时区问题
ENV TZ "Asia/Shanghai"
ENV TERM xterm

