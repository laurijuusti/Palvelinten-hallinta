# Raportti 2, Karjaa (Saturday 4.11.2023)

### OS: MacOS 14.0 Sonoma
### Kone: 13" MacBook Pro 2021 (M1, 8GB RAM)

## x) Lue ja tiivistä (klo. 20.26)

 - Cattle-mindset servereissä on ikään kuin sama asia kuin karjaa, jos jokin palvelin kymmenistä tai sadoista menee alas tai rikki, se on nopeasti ja helposti korvattavissa.
 - Vagrantilla saa alle minuutissa virtuaalikoneen pystyyn johon saa SSH-yhteyden ja sen voi tuhota tarvittaessa.
 - Kolmannessa artikkelissa puhuttiin kuinka Vagrantilla saa automaattisesti luotua kolme konetta, hyväksyä "orjat", ajaa niillä komentoja ja lopuksi tuhota ne. 


## a) Vagrantin asennus

Vagrantin saa asennettua Macille komennolla 

     brew install hashicorp/tap/hashicorp-vagrant

Jos laitteella ei ole Homebrewiä (paketinhallinta Macille) asennettuna, saa sen komennolla 

     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

Komennon lopputulos, Vagrant 2.4.0 on asennettu!

<img width="932" alt="image" src="https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/ab0b6802-7d47-434e-9026-308202b767a9">

## b) Yksi maankiertäjä

Spesifioin vagrantille Debian 11 "Bullseye"n, komennolla, ja käynnistin koneen komennolla 

    vagrant init debian/bullseye64, vagrant up
     
<img width="657" alt="image" src="https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/e3415b7f-678a-4716-b5d8-105714487807">

Sain errorin että ei ole virtualisointiohjelmaa, ja kävin lataamassa VirtualBoxin sivulta https://www.virtualbox.org/wiki/Testbuilds kohdan MacOS ARM64 BETA alta:

<img width="716" alt="image" src="https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/3cbbc2dc-0396-4a7c-a487-e73d2cbcbd93">

Asennus onnistui, voimme jatkaa.

Sain virtuaalikoneesta errorin "CPU Model not supported" 

<img width="330" alt="image" src="https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/6aa41b6a-86c8-4924-81a0-7b84e8831152">

Kokeilin löytämääni Ubuntu boxia näillä ohjeilla, ajoin komennot ja lopputuloksena oli "Machine booted and ready!": 
Providerina siis QEMU, ei VirtualBox.

<img width="1056" alt="image" src="https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/21c2373d-ca9e-4988-adad-841333524e22">

SSH:tin sisään komennolla "vagrant ssh". Netti toimii jotenkin :D 

<img width="922" alt="image" src="https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/cb02755c-0b11-4d49-9292-6a2434a1e28f">

## c) Oma orjansa

Päivitin ubuntun paketit: "sudo apt upgrade" sekä "sudo apt install"

Asensin Saltin herran sekä orjan komennoilla "sudo apt install salt-master" sekä "sudo apt install salt-minion".

## d) 






   


## Tiivistelmä, lähteet (klo. 21.11)



Lähteet:

https://www.virtualbox.org/wiki/Testbuilds

https://terokarvinen.com/2023/salt-vagrant/

https://terokarvinen.com/2023/configuration-management-2023-autumn/

https://app.vagrantup.com/perk/boxes/ubuntu-2204-arm64







