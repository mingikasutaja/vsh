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
</html> ```
