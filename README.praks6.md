# Praktikum 6

## Andmebaasi server

Andmebaasi serverile paigaldasin mariadb-server ning käivitasin mysql installationi käsuga

```apt-get install mariadb-server```

```mysql_secure_installation```

Mysql installatsioonis panin kõigele peale parooli vahetamist valiku ```yes```

Järgmisena muutsin /etc/mysql/my.cnf failis bind-address rea ära ning sisestasin andmebaasi serveri ip, milleks oli 10.0.2.7

Peale seda tegin mysql teenusele restarti.

Seejärel sisenesin mysqli sisse ning sisestasin käsud

```
CREATE DATABASE wordpress;
CREATE USER 'WPuser'@'localhost' IDENTIFIED BY 'qwerty';
GRANT ALL PRIVILEGES ON wordpress.* TO 'WPuser'@'localhost';
CREATE USER 'WPuser'@'10.0.2.6' IDENTIFIED BY 'qwerty';
GRANT ALL PRIVILEGES ON wordpress.* TO 'WPuser'@'10.0.2.6';
exit;
```
## Wordpressi server

Selle paigaldamiseks tegin apt update ja paigaldasin apache2 ning mariadb-client ja php-mysql ning alla sai ka veel laetud zip käsk.

Järgmisena sisestasin sources.listi
```
deb http://packages.dotdeb.org jessie all
deb-src http://packages.dotdeb.org jessie all
```
ning tegin ```apt install php7.0-*```

peale seda tegin ```service apache2 reload```

Järgmisena läksin /tmp kausta ning laadisin alla wordpressi ja pakkisin selle lahti käskudega
```
cd /tmp
wget -c http://wordpress.org/latest.zip
unzip -q latest.zip -d /var/www/html/
```
Seejärel määrasin õigused ja tegin vajalikud kaustad jne
```
chown -R www-data.www-data /var/www/html/wordpress
chmod -R 755 /var/www/html/wordpress
mkdir -p /var/www/html/wordpress/wp-content/uploads
chown -R www-data.www-data /var/www/html/wordpress/wp-content/uploads
```
```
cd /var/www/html/wordpress/
cp wp-config-sample.php wp-config.php
nano wp-config.php
```
wp-config.php failis muutsin ära useri, passwordi, database name ja ka hostname. hostname kohale panin 10.0.2.7

## Ubuntu klient

Kliendi arvutile paigaldasin ubuntu 18.04 ja määrasin sellele 2GB RAM ja 25GB ketast.
