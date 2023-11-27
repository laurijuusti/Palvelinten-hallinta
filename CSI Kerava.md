# Raportti 5, CSI Kerava (Maanantai 27.11.2023)

### OS: Windows 10 22H2 64-bit
### Kone: i5-10300H, 8GB RAM

## x) Lue ja tiivistä (klo. 13.31)

  - Artikkelissa puhuttiin Apachen asentamisesta ja käyttäjän kotisivujen muokkaamisesta Saltilla automaattisesti. 
  
## a) CSI Kerava (klo 13.37)

Ajoin komennon "sudo find /etc/ -mtime -1 -printf "%A+ %f %n\n", joka tulostaa kansiosta /etc/ viime 24h aikana muokatut tiedostot ja formatoi ne muokkausajan, tiedoston nimen ja number of hard linkkien mukaan, kaikki eri riveille /(%a+, %f, %n sekä \n). 

Hard linkit meinaavat periaatteessa vissiin sitä, kuinka monta kertaa tiedosto esiintyy levyllä. 
Komento löysi 6 tiedostoa, jotain cacheja, firefoxin yms.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/ba6e5a89-90b0-4afb-8dee-c23310dade34)

## b) Gui2fs (klo. 13.59)

Navigoin kansioon ~/.mozilla/firefox/z4u4bks3.default-esr/, ja avasin tiedoston "prefs.js", joka näytti omaan silmään asetustiedostolta. Samalla vaihdoin Firefoxista hakukoneekseni DuckDuckGon (oikea yläkulma firefoxissa -> hampparivalikko -> settings -> search -> default search engine -> duckduckgo)

Sen sisällä oli monta eri asetusta, noin 160 riviä. Nyt siellä näkyy eräissä rivissä jotain DuckDuckGohun viittaavaa, eli oletan että muutos vaikutti tähän. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/47ba530f-56b6-45d8-9205-a16d4ca78955)

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/5ac813ca-236e-464f-b159-c2e5213e5c40)

## c) Komennus

Loin kansion /srv/salt/testi1/ komennolla "sudo mkdir -p /srv/salt/testi1/". Loin kansioon tiedoston init.sls, jossa on seuraava sisältö:

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/314aaa1a-a07f-4419-8965-c79d777930a3)

Tämä tila asentaa paketin 'neofetch' koneelle. Ajoin tilan komennolla "sudo salt-call --local state.apply testi1", ja sain viestin että paketti on asennettu jo. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/a01e4dda-9d9d-4f39-8274-f408c2eee590)

## d) Apassi

Virtuaalikoneellani on jo Apache asennettuna aiemmista tehtävistä. Ensimmäiseksi enabloin käyttäjien kotisivut komennoilla "sudo a2enmod userdir" ja "sudo systemctl restart apache2".

Loin kansion "public_html", ja sinne index.html:än jossa on vähän sisältöä. Näkyy selaimessa, käsin asennus toimii. Kokeillaan Saltilla seuraavaksi käyttäen Teron valmiiksi luomaa infra-as-code tiedostoa. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/b9ffca1d-d8ce-40e9-b7a1-6d771aa3f3f6)

Loin kansion /srv/salt/apache/, jossa on init.sls tiedostossa seuraava sisältö:

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/baffed57-6f36-40ac-be73-731476a1920d)

Kokeilin statea komennolla "sudo salt-call --local state.apply apache", ja sain seuraavan tuloksen. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/5041b304-e98c-45ca-8e5f-0046688f5432)



## e) Ämpärillinen






## Tiivistelmä, lähteet



Lähteet:

https://terokarvinen.com/2023/configuration-management-2023-autumn/

https://terokarvinen.com/2018/04/03/apache-user-homepages-automatically-salt-package-file-service-example/

https://www.cbtnuggets.com/blog/certifications/open-source/linux-hard-links-versus-soft-links-explained

https://github.com/laurijuusti/Palvelinten-hallinta/blob/main/Demonit.md
