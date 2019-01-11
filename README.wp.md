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
      
