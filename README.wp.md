# Praktikum 3
## Installeerisin PHP5
```apt-get install php libapache2-mod-php php-mcrypt php-mysql```
## Installeerisin MYSQL server
```apt-get install mysql-server```
## Installeerisin Phpmyadmin teenuse
```apt-get install -y phpmyadmin```
Tee ära installatsioon ja konfiguratsioon
Peale seda enablei mcrypt moodul kui seda juba ei kasutata
Kõigepealt kontrolli kas see töötab käsuga
 ```php -m | grep mcrypt ```
 Kui midagi ei juhtu siis kasuta käsku ```php5enmod mcrypt```
  
  Tõestus et asi töötab asub siin
  vsh/scrteenshot1.PNG
  
 ##PHP lehe paigaldamine
 tegin faili nimega index.php kohta /var/www/html kuhu sisestasin rea
 ```<?php phpinfo(); ?>```
 Tõestus et asi töötab asub siin
 vsh/screenshot2.PNG
 kasutaja lehe tegemiseks tegin faili test.php kohta /var/www/public_html/ ning selle sisse kirjutasin read
```
<html>
<head>
<title> Testin asja PHP</title>
</head>
<body>
<?php echo '<p> avalik leht </p>'; ?>
</body>
</html>
```
Peale seda oli vaja ära muuta /etc/apache2/mods-enabled/php5.conf failis vaja ära muuta keelatud php moodulid (viimased viis rida) ning panna nad kommentaarideks
# HTTPS konfigureerimine apache2 veebiserverile

## Võtme genereerimine
Kõigepealt lõin endale uue kausta kuhu ma oma sertifikaadid panin ```mkdir /etc/apache2/ssl```
Siis genereerisin endale sertifikaadi 1095 päevaks ehk kolmeks aastaks käsuga ```openssl req -x509 -nodes -days 1095 -newkey rsa:2048 -out /etc/apache2/ssl/server.crt -keyout /etc/apache2/ssl/server.key```
Mis omakorda näitas järgnevat
```
Generating a 2048 bit RSA private key
............................................+++
.....................+++
writing new private key to '/etc/apache2/ssl/server.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:EE
State or Province Name (full name) [Some-State]:Estonia
Locality Name (eg, city) []:
Organization Name (eg, company) [Internet Widgits Pty Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:172.23.13.43
Email Address []:
```
Kõige tähtsam koht selles asjas oli ```Common Name``` kus tuli määrata oma veebilehe aadress. Mina panin sinna oma veebilehe ip aadressi
## Faili konfigureerimine ja linkimine
Installisin SSL modi apachele käsuga ```a2enmod ssl```

Siis linkisin kaks asja omavahel
```ln -s /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-enabled/000-default-ssl.conf```

Nüüd avasin konfigureerimist vajava faili ```nano /etc/apache2/sites-enabled/000-default-ssl.conf```

Ja muutsin need read ära selliseks
```
SSLCertificateFile    /etc/apache2/ssl/server.crt
SSLCertificateKeyFile /etc/apache2/ssl/server.key
```

