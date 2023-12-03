# Raportti 5, CSI Kerava (Maanantai 27.11.2023)

### OS: Windows 10 22H2 64-bit
### Kone: AMD Ryzen 7 3700x, 32GB DDR4 RAM, RTX 3080

## x) Lue ja tiivistä (klo. 21.40)

 Valitsin artikkeliksi Tuomas Valkamon "Using Salt with Windows" https://tuomasvalkamo.com/CMS-course/week-5/ (Tuomas Valkamo 1.12.2022). Artikkelissa puhuttiin tietenkin Saltin käytöstä Windows virtuaalikoneessa, komentojen ajamisesta ja porttien aukinaisuuden katsomisesta. 

Toisessa artikkelissa puhuttiin Windows-virtuaalikoneen luomisesta VirtualBox-sovelluksella. 

Kolmannessa artikkelissa käsiteltiin Linuxin filesystemiä kattavasti. Käytiin läpi esim. erilaisia kansioita ja mitä tiedostoja niihin kuuluu. Itse käyttänyt esim. /srv, /tmp, /ja tietenkin /usr

## a) Asenna Windows virtuaalikoneeseen (klo. 21.50)

Laitoin 64-bittisen .iso-tiedoston lataamaan linkistä https://go.microsoft.com/fwlink/p/?LinkID=2208844&clcid=0x809&culture=en-gb&country=GB. Kielivalintana GB. Softana käytän VMWare Workstation 17 Player. Sen käynnistettyä painoin alkuruudusta 'Create new Virtual Machine'. Spesifioin .ison ja painoin Next.  

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/4eecce6d-2157-4987-a4a3-275bfcb495de)

Seuraavaan ruutuun missä kysyttiin tuoteavainta en laittanut mitään ja painoin next. Siitäkin seuraavasta ruudusta painoin Next ja annoin 60 GB tilaa. Painoin taas next. Seuraavasta ruudusta valitsin 'Customize Hardware ja annoin sille 4 CPU-säiettä ja 8GB RAMia. Painoin Finish ja VM käynnistyi. 

Pääsin setuppiin ja painoin next. ![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/74f69acd-0888-4807-b99f-67407e53c068)

Sain erroria License termeistä, kokeillaan vaihtaa VirtualBoxiin. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/e59cc162-5851-472c-996b-19ec72ad710f)

Samat speksit kuin äsken, 50GB Disk. ![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/efb95b3a-54a7-45b0-8f05-ea7cf3749a9f). Vieläkin sama vika. ![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/1bf026c2-f0dd-4c8c-9340-b22e6f0cab1b)

Kokeillaan uudestaan, nyt on asetus 'Skip Unattended Installation' päällä. Annan koneelle myös 16GB RAM ja 8 CPU-säiettä ![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/ba2bdb3f-e20f-41a0-aec1-a7e7ff5845d7)

Noniin! ![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/037e5f68-f7d4-4a24-8d92-97071d441257) Ensin kielivalinnat ja seuraavasta ruudusta 'Install Now'. Hyväksyin EULA:n ja valitsin 'Custom: Install Windows Only'. Valitsin tyhjän virtuaalilevyn ja painoin Next. VM autorestarttasi muutaman kerran ja lopulta pääsin sisään. Varmistin vielä alueen ja näppäimistön Suomeksi. Valitsin 'Domain join instead, kun sain ruudun liittyä Microsoft-tilillä koska niin en halua tehdä. Nimeksi laitoin L. Pääsin sitten 'yksityisasetuksiin', joihin kaikkiin valitsin No. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/52156295-c2bd-48a4-b88e-029591091cf0)




## b) Asenna Salt


## c) Kokeile grains.items


## d) Kokeile File

## e) Kokeile jotain uutta toimintoa. 

## Tiivistelmä, lähteet (klo. )

Artikkelissa asensin Windowsin virtuaalikoneelle, asensin siihen Saltin ja leikin sillä hieman.

### Lähteet:

https://terokarvinen.com/2023/configuration-management-2023-autumn/

https://tuomasvalkamo.com/CMS-course/week-5/
