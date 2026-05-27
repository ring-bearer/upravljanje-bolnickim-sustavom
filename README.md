# Upravljanje bolničkim sustavom

Web aplikacija za upravljanje bolničkim pregledima, terminima i zahtjevima pacijenata izrađena u sklopu kolegija Napredne baze podataka na Prirodoslovno-matematičkom fakultetu Sveučilišta u Zagrebu.

Aplikacija omogućuje pacijentima, liječnicima i administratorima pristup sustavu kroz različite razine ovlasti. Pacijenti mogu slati zahtjeve za pretrage, liječnici ih mogu odobravati ili odbijati, dok administratori imaju pregled i kontrolu nad svim podacima u sustavu.

Sustav koristi relacijsku bazu podataka PostgreSQL s implementiranim SQL funkcijama, indeksima i logikom za raspoređivanje termina i pronalazak obližnjih bolnica.

---

## Funkcionalnosti

### Autentifikacija i ovlasti
- prijava korisnika u sustav
- različite razine pristupa:
  - pacijent
  - liječnik
  - administrator

### Upravljanje pregledima i terminima
- slanje zahtjeva za pretrage
- odobravanje i odbijanje zahtjeva
- pregled povijesti pretraga
- pregled nadolazećih termina
- automatsko predlaganje prvih slobodnih termina

### Sustav preporuke bolnica
- pronalazak obližnjih bolnica na temelju geografske udaljenosti
- prikaz najranijih dostupnih termina za traženu pretragu

### Funkcionalnosti baze podataka
- relacijski model baze podataka
- PostgreSQL funkcije i procedure
- indeksiranje za optimizaciju upita
- implementacija logike raspoređivanja termina u PL/pgSQL-u

### Arhitektura aplikacije
- MVC arhitektura u PHP-u
- povezivanje PHP aplikacije s PostgreSQL bazom pomoću PDO-a

---

## Tehnologije

- PHP
- PostgreSQL
- SQL / PLpgSQL
- PDO
- MVC arhitektura
- Git / GitHub

---

Web aplikaciji moze se pristupiti sa lokalnog hosta.
Potrebno je imati PHP i instaliran driver za njegov rad s Postgresom.\
Korisne naredbe (na Linuxu preko terminala):
- instalacija PHP-a: ```sudo apt-get install php```
- provjera instalirane verzije PHP-a: ```php --version```
- instalacija drivera za Postgres: ```sudo apt-get install php-pgsql``` ili ako imate npr. PHP verziju 7.4, ```sudo apt-get install php7.4-pgsql```
- pronalazak datoteke php.ini: ```sudo find / -name php.ini```

U slučaju da Postgres driver ne radi nakon instalacije, potrebno je u php.ini odkomentirati sljedeće linije:
 - ```extension=pgsql```
 - ```extension=pdo_pgsql```

Za relacijsku bazu, povezujemo se s bazom odbojka kao za prvu i drugu zadaću. Nakon dobivanja konekcije s virtualkom na VCLu, potrebno je dobiveni IP prekopirati u app/database/db.class.php, kod imena host-a.
Tad se za brzu inicijalizaciju baze može pristupiti prepareDB.php preko web-a (adresa oblika http://localhost/~username/nbp/app/database/prepareDB.php).
Nakon toga, korisnik bi uvijek trebao pristupati samo datoteci index.php, koja će ga preusmjeriti na traženi sadržaj (http://localhost/~username/nbp/index.php).
