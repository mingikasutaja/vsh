# Dokuwiki installatsioon
Kasutasin järgmist juhendit https://www.dokuwiki.org/install:debian
## Lighttpd

Kõigepealt tegin ```apt-get update``` ```apt-get install lighttpd```	 ja ```apt-get install php5-cgi php5 dokuwiki```
lighty-enable-mod fastcgi fastcgi-php dokuwiki	 /​etc/​init.d/​lighttpd force-reload




## nginx
```/etc/nginx/sites-enabled/default```

```
 # serve static files from nginx
    location ~ ^/dokuwiki/lib/.+\.(css|gif|js|png)$ {
        root /usr/share;
        expires 30d;
    }
    location = /dokuwiki/install.php {
        deny all;
    }
    location = /dokuwiki {
        rewrite ^ /dokuwiki/ permanent;
    }
    location = /dokuwiki/ {
        rewrite ^ /dokuwiki/doku.php last;
        expires 30d;
    }
    location ~ ^/dokuwiki/(|lib/(exe|plugins/[^/]+)/)[^/]+\.php {
        root /usr/share;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        include        fastcgi_params;
        # from Debian Jessie, replace the previous include by
        include snippets/fastcgi-php.conf;
    }
    location /dokuwiki/ {
        deny all;
    }
```
## Apache
```sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt dokuwiki```
Kui valid valiku "yes" siis PHP installeerib iseennast
Kui sa näed lihtsalt "It works" lehte või midagi sarnast siis tee kindlaks et default index.html oleks eemaldatud saidi kaustast.


Järgmiseks sisesta järgmine käst ```nano /etc/apache2/mods-enabled/dir.conf```
ning sisesta sinna järgmine rida
```
<IfModule mod_dir.c>
          DirectoryIndex index.php index.html index.cgi index.pl index.php index.xhtml index.htm
</IfModule>
```
järgmiseks on vaja kaks vaili ainult linkida ja siis ongi kõik
```ls -l /etc/apache2/conf-available/```
```ls -l /etc/apache2/conf-enabled/```
Apache konfiguratsiooni failist (dokuwiki.conf või apache.conf) tuleb ```Alias``` ja ```Allow from localhost 127.0.0.1 ::1```
muuta endale sobivaks. Default lubab ainult hostist vaadata dokuwikit kuid ```Allow from all``` lubab ükskõik kellel seda vaadata
