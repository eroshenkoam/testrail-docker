FROM php:5.6-apache

ENV PHP_VERSION 5.6

RUN \
    apt-get update && \
    apt-get install -y zip && \
    apt-get install -y wget && \
    apt-get install -y unzip && \
    apt-get install -y zlib1g-dev && \
    apt-get install -y libcurl4-gnutls-dev && \
    docker-php-ext-install mysql && \
    docker-php-ext-install curl && \
    docker-php-ext-install zip && \
    rm -rf /var/lib/apt/lists/*

ENV IONCUBE_VERSION 5.1.2

RUN \
  wget  -O /tmp/ioncube.tar.gz http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64_${IONCUBE_VERSION}.tar.gz && \
  tar -xzf /tmp/ioncube.tar.gz -C /tmp && \
  mv /tmp/ioncube /opt/ioncube && \
  echo zend_extension=/opt/ioncube/ioncube_loader_lin_${PHP_VERSION}.so >> /usr/local/etc/php/php.ini && \
  rm -f /tmp/ioncube.tar.gz

RUN \
  wget -O /tmp/testrail.zip http://www.gurock.com/downloads/testrail/testrail-latest-ion53.zip && \
  mkdir -p /var/www/testrail && \
  unzip /tmp/testrail.zip -d /tmp && \
  mv /tmp/testrail/* /var/www/html/ && \
  mkdir -p /var/www/html/logs && chown www-data:www-data /var/www/html/logs && \
  mkdir /etc/cron.d && echo '* * * * * www-data /usr/bin/php /var/www/html/task.php' >> /etc/cron.d/testrail && chmod +x /etc/cron.d/testrail

VOLUME /opt/testrail/attachments
VOLUME /opt/testrail/reports

EXPOSE 80