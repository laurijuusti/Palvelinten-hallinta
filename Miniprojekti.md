# Miniprojekti (Sunnuntai 10.12.2023)

### OS: Windows 10 22H2 64-bit
### Kone: AMD Ryzen 7 3700x, 32GB RAM, RTX 3080
  
## a) Miniprojekti


Loin itselleni ensin testiympäristön kahdesta Debian 11 virtuaalikoneesta käyttäen Vagrantia ja Tero Karvisen luomaa vagrantfileä, jonka muokkasin luomaan herran ja yhden orjan. Sain tämän toiminaan komennoilla      

    $ vagrant init debian/bullseye64, vagrant up

Vagrantfile asentaa orjalle valmiiksi paketin "salt-minion".

Vagrantfilen sisältö:

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/b1c48bc9-993f-48f0-bb57-a1126a3d93de)

SSH:tin itseni masterille, hyväksyin avaimet sekä testasin että herra-orja arkkitehtuuri on pystyssä. 

    $ vagrant ssh tmaster, sudo salt-key -A, sudo salt '*' test.ping
    
![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/8f5a8f75-fc29-4bbf-b907-c73d279c77bc)


## Tiivistelmä, lähteet


Lähteet:

https://terokarvinen.com/2023/configuration-management-2023-autumn/


