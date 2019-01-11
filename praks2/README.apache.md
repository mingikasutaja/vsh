# Oli vaja kloonida masin mille nimeks määrasin apache
Apache masinasse kloonisin vsh repositoorium githubist
git clone https://github.com/mingikasutaja/vsh

minu kasutaja githubis ongi mingikasutaja

# Tekkinud vsh kataloogis lõin kausta nimega praks2
mkdir praks2

# Paigaldasin apache2 veebiserver
apt-get install apache2

# Lisasin oma andmed apache veebilehele
## Kõigepealt tühjendasin faili käsuga var/www kaustas
truncate -s 0 index.html
## lisasin järgmised asjad index.html faili
 ```<!DOCTYPE html>
<html>
<head>
<title>Erik Sarik veebileht</title>
</head>
<body>

<h1>Erik Sarik veebileht</h1>
<h2>ISP217</h2>
<p>erik.sarik@khk.ee</p>

</body>
</html> 
```

# Avaliku kausta tegemine veebilehele
Alguses kasutasin käsku 
```mkdir /home/it/public_html```
Siis linkisin selle /var/www kaustaga käsuga
```ln -s /home/it/public_html/ /var/www```
Peale seda oli vaja lubada kasutaja kaustad ning selleks kasutasin käsku
```a2enmod userdir```
peale seda tegin apache2 teenusele restarti käsuga
```service apache2 restart```
