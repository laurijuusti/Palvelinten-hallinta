# Raportti 6, Windows (Sunnuntai 3.12.2023)

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

Samat speksit kuin äsken, 50GB Disk. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/efb95b3a-54a7-45b0-8f05-ea7cf3749a9f). 

Vieläkin sama vika. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/1bf026c2-f0dd-4c8c-9340-b22e6f0cab1b)

Kokeillaan uudestaan, nyt on asetus 'Skip Unattended Installation' päällä. Annan koneelle myös 16GB RAM ja 8 CPU-säiettä.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/ba2bdb3f-e20f-41a0-aec1-a7e7ff5845d7)

Noniin! 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/037e5f68-f7d4-4a24-8d92-97071d441257) 

Ensin kielivalinnat ja seuraavasta ruudusta 'Install Now'. Hyväksyin EULA:n ja valitsin 'Custom: Install Windows Only'. Valitsin tyhjän virtuaalilevyn ja painoin Next. VM autorestarttasi muutaman kerran ja lopulta pääsin sisään. Varmistin vielä alueen ja näppäimistön Suomeksi. Valitsin 'Domain join instead, kun sain ruudun liittyä Microsoft-tilillä koska niin en halua tehdä. Nimeksi laitoin 'L', ei salasanaa tällä kertaa (2 kertaa Enter-painiketta kun kysyy salasanaa). Pääsin sitten 'yksityisasetuksiin', joihin kaikkiin valitsin No. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/52156295-c2bd-48a4-b88e-029591091cf0)

Vihdoin työpöydällä...

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/c965aa63-9577-433b-a761-d72f5367083e)


## b) Asenna Salt

Googlasin 'Salt Windows', ja avasin linkin https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/windows.html. Valitsin 'Download Install File' (AMD64, .Exe).

Avasin tiedoston ja valitsin Yes.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/ced4f3c8-3f1e-4aa1-88d2-f518ba87806d)

Installerissa valitsin Next, I agree, valitsin oletuskansion ja Next, hostnamelle ja minionin nimelle myös defaultit. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/eb32f5d1-2c79-45e7-aacb-455ec35f4ebb)

Sain promptin asentaa VCRedist_x64_2013, asensin senkin valitsemalla Yes.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/66a57d88-a9c3-4078-95b9-601bb5e4893c)

Lopetin asennuksen painamalla Finish.

Salt on asennettu!

## c) Kokeile grains.items

Avasin powershellin painamalla Win + X -> Windows Powershell (Admin).

Varmistin vielä saltin olemassaolon "salt-call --version".

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/6ca7d102-6c28-4437-aedc-a8caf2aa8608)

Ajoin komennon *salt-call --local info grains.items", ja sieltähän tiedot tulivat!

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/7906b93b-44f3-4171-b4ac-b553b2a1c262)

## d) Kokeile File

Loin init.sls tiedoston kansioon C:/Users/L/Salt/Test, jossa on seuraava sisältö: 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/8cecb719-4f24-4561-91f4-2b6ae433c228)

Ajetaan tämä Valkamon ohjeiden mukaan komennolla "salt-call --file-root=C:/Users/L/Salt/Test --local state.apply File-test", jossa --file-root kertoo Saltille kansion jota käyttää. Komento ei minulla toiminut, se ei löytänyt sitä .sls filua jostain syystä :/

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/a95baaa9-985e-4a47-b100-7bfbe5ab442a)


## e) Kokeile jotain uutta toimintoa. 

Löysin toiminnon jolla voi vaihtaa koneen kuvausta, kokeilin sitä: "salt-call --local system.set_computer_desc"

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/0d4faa78-25d1-4b45-ba49-4bfc39d1c0dc) 

Näyttäisi pelaavan.

## Tiivistelmä, lähteet (klo. 23.12)

Artikkelissa asensin Windowsin virtuaalikoneelle, asensin siihen Saltin ja leikin sillä hieman (vähän epäonnistuneesti :D).

### Lähteet:

https://terokarvinen.com/2023/configuration-management-2023-autumn/

https://tuomasvalkamo.com/CMS-course/week-5/
