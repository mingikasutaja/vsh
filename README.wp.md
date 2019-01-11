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
