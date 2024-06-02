# Ausgangsimage Ubuntu 20.04 verwenden
FROM ubuntu:20.04

# Setzt den DEBIAN_FRONTEND auf noninteractive, um interaktive Eingaben zu vermeiden
ENV DEBIAN_FRONTEND=noninteractive

# Aktualisiert die Paketlisten und installiert software-properties-common
RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update && apt-get install -y \
    apache2 \
    php8.1 \
    php8.1-mysql \
    php8.1-xml \
    php8.1-curl \
    php8.1-gd \
    php8.1-intl \
    php8.1-xmlrpc \
    php8.1-ldap \
    php8.1-zip \
    php8.1-soap \
    php8.1-mbstring \
    libapache2-mod-php8.1 \
    graphviz \
    aspell \
    ghostscript \
    clamav \
    git \
    curl \
    vim \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*
 
# Moodle von GitHub herunterladen und im Verzeichnis /var/www/html/moodle installieren
RUN git clone -b MOODLE_401_STABLE git://git.moodle.org/moodle.git /var/www/html/moodle
 
# Create moodledata directory and set permissions moodledata Verzeichnis erstellen und Berechitgung setztn.
RUN mkdir -p /var/www/html/moodledata && \
    chown -R www-data:www-data /var/www/html/moodle && \
    chown -R www-data:www-data /var/www/html/moodledata && \
    chmod -R 775 /var/www/html/moodle && \
    chmod -R 775 /var/www/html/moodledata
 
# PHP-Einstellungen anpassen
RUN sed -i 's/;max_input_vars = 1000/max_input_vars = 5000/' /etc/php/8.1/apache2/php.ini    
 
# Apache Seite anpassen
RUN sed -i 's|/var/www/html|/var/www/html/moodle|' /etc/apache2/sites-available/000-default.conf && \
    echo '<Directory "/var/www/html/moodle">' >> /etc/apache2/sites-available/000-default.conf && \
    echo '    AllowOverride All' >> /etc/apache2/sites-available/000-default.conf && \
    echo '    Require all granted' >> /etc/apache2/sites-available/000-default.conf && \
    echo '</Directory>' >> /etc/apache2/sites-available/000-default.conf && \
    a2enmod rewrite && \
    service apache2 restart
 
# Ports 80 und 443 freigeben
EXPOSE 80 443
 
# Apache im Vordergrund starten
CMD ["apache2ctl", "-DFOREGROUND"]