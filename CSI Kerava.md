# Raportti 5, CSI Kerava (Maanantai 27.11.2023)

### OS: Windows 10 22H2 64-bit
### Kone: i5-10300H, 8GB RAM

## x) Lue ja tiivistä (klo. 13.31)

  - Artikkelissa puhuttiin Apachen asentamisesta ja käyttäjän kotisivujen muokkaamisesta Saltilla automaattisesti. 
  
## a) CSI Kerava

Ajoin komennon "sudo find /etc/ -mtime -1 -printf "%A+ %f %n\n", joka tulostaa kansiosta /etc/ viime 24h aikana muokatut tiedostot ja formatoi ne muokkausajan, tiedoston nimen ja number of hard linkkien mukaan, kaikki eri riveille /(%a+, %f, %n sekä \n). Hard linkit meinaavat periaatteessa vissiin sitä, kuinka monta kertaa tiedosto esiintyy levyllä. 
Komento löysi 6 tiedostoa, jotain cacheja, firefoxin yms.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/ba6e5a89-90b0-4afb-8dee-c23310dade34)

## b) Gui2fs






## c) Komennus






## d) Apassi






## e) Ämpärillinen






## Tiivistelmä, lähteet



Lähteet:

https://terokarvinen.com/2023/configuration-management-2023-autumn/

https://terokarvinen.com/2018/04/03/apache-user-homepages-automatically-salt-package-file-service-example/

https://www.cbtnuggets.com/blog/certifications/open-source/linux-hard-links-versus-soft-links-explained

