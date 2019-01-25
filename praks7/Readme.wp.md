# Dokuwiki installatsioon
Kõigepealt tegin ```apt-get update``` ```apt-get install lighttpd```	 ja ```apt-get install php5-cgi php5 dokuwiki	 ```
```lighty-enable-mod fastcgi fastcgi-php dokuwiki	 
/​etc/​init.d/​lighttpd force-reload```
## Lighttpd
```/etc/nginx/sites-enabled/default```


```  # serve static files from nginx
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
    }```
