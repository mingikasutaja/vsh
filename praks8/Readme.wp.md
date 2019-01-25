# Nimelahendus

Virtual hosts ehk nimelahendus

Alustuseks tegin uue kausta nimega erik.ee asukohta /var/www/ ning sinna sisse tegin index.html faili. Kaustadele andsin õigused käskudega
```
chown -R www-data /var/www/erik.ee
chgrp -R www-data /var/www/erik.ee~
```
Peale seda pidi kopeerima apache2 default konfiguratsiooni asukohast: /etc/apache2/sites-available/000-default.conf Asukohta /etc/apache2/sites-available/apache.erik.conf

Avasin uue tehtud faili ning muutsin järgmised read:
```
DocumentRoot /var/www/erik.ee
ServerName apache.erik.ee
ServerAlias erik.ee
DocumentRoot /var/www/html/www ##
        <Directory />
                Options FollowSymLinks
                AllowOverride None
        </Directory>
        <Directory /var/www/html/www> ##
                Options Indexes FollowSymLinks MultiViews
                AllowOverride None
                Order allow,deny
                allow from all
        </Directory>
```
Kõik muu jätsin samaks Nüüd pidi lehekülje lubama ja käivitama Käsuga:

a2ensite apache.erik.ee ning peale seda

service apache2 restart Kui vajalik siis peab ka minema faili /etc/hosts ning sinna lisama rea (sinu VMi IP) apache.erik.ee Peale seda restart apachele ning lehekülg peaks töötama.
