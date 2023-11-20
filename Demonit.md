
# Raportti 4, Demonit (Maanantai 20.11.2023)

### OS: Windows 10 22H2 64-bit
### Kone: AMD Ryzen 7 3700x, NVIDIA RTX 3080, 32GB DDR4 RAM

## x) Lue ja tiivistä

Karvinen 2023:
  - Artikkelissa näytetään kuinka luodaan Salttiin init.sls-tiedosto johon laitetaan sisältöä joka luo kansion /tmp/infra-as-code/, ja laitetaan muutos toimimaan.
  - Toisessa kohdassa näytetään top file, joka automaattisesti laittaa spesifioidut infra-as-code tekstitiedostot päälle orjille, kun annetaan vain komento "state.apply".

Salt Project:
  - Kohdassa mainitaan YAMLin säännöistä, kuten ei tabeja, kommentit alkavat risuaidalla, kaikki on case-sensitive, data strukturoidaan avain: arvo-pareihin, yms.
  -  Kerrotaan myös YAMLin kolmesta perus elementtityypeistä: Scalars, Lists and Dictionaries, ja mitä ne ovat.
  -  Kerrotaan myös siitä, miten YAML koostuu. Indentaatio on tärkeää, ja jokainen tieto alkaa "- " merkeillä jolla indikoidaan jokaista merkintää
  -  Kolmannessa kohdassa avataan Saltin moduuleja (millaista on tarkistaa pakettien asennus Saltilla ja ilman)
      -  Näytetään esimerkki Saltin SLS-tiedoston data struktuurista,
      -  Kerrotaan sls-tiedoston organisoinnista ja simppelinä pidosta
      -  Kerrotaan vähän miten Salt auttaa organisaatioita ison skaalan operaatioissa, yksi apu tähän on top.sls-tiedosto
      -  Ja viimeisenä näytetään Apachen ja SSHD:n infra-as-code init.sls-tiedostot.

Karvinen 2018:
  - Artikkelissa näytetään SSHD:n konffaus portille 8888.

## a) Hello SLS!

Tein raporttini Karjaa ohjeiden mukaan Vagrantilla testiympäristön, jossa on kaksi orjaa ja yksi herra. SSH:tin itseni sisään komennolla "vagrant ssh tmaster".

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/7d7b0187-8496-4843-a470-bcbfe392fb07)

Loin kansion /srv/salt/hello, johon loin tiedoston init.sls, jossa on seuraava sisältö:

`/tmp/infra-as-code:
  file.managed ` GitHubin formatointi ei näytä preview-modessa tätä oikein, pitäisi olla rivien välissä enter + 2 välilyöntiä.

Kun tuon muutoksen tekee, tämän pitäisi luoda orjien tmp-kansioon kansio jonka nimi on infra-as-code. Kokeillaan.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/98d33707-65a5-4bb2-88c3-bfa267d82749)

Minioneihin ei näköjään saa yhteyttä, kokeillaampas hyväksyä avaimet:

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/c6aec705-7c20-49ad-92a8-37702bcae861)

Nyt pitäisi toimia. "sudo salt-key -A" sekä "sudo salt '*' test.ping". Kokeillaan uudelleen. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/eacc3124-141c-4b19-8d7a-cc823991f85a)

Kansio luotu molempiin, käydäämpäs vielä tarkistamassa orjilta. Siellähän se on.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/9ecd7bee-fdb1-4d03-8d2d-e01b6bfd737b)


## b) Top

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/12fab51f-5e96-43a9-b92c-9b55dff98309)

Laitoin seuraavan sisällön tiedostoon /srv/salt/top.sls

Ajoin muutokset komennolla "sudo salt '*' state.apply". Huomaa, että nyt ei tarvitse spesifioida nimeä, eli sitä helloa. Muutoksia ei tehty, koska komennot ovat indemponttisia, ja kansio oli jo siellä. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/5632c03b-45ff-451a-9f00-3a673bf195da)



## c) Apache

Asensin apachen käsin komennolla "sudo apt update", sekä "sudo apt install apache2".

Kokeilin curlata localhostin, mutta curlia ei ollut virtuaalikoneessa. Asensin senkin komennolla "sudo apt install curl".

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/b86a0e22-71c3-4230-b833-904ac405b0de)

Curlasin uudelleen komennolla "curl localhost", ja sieltähän tuli apachen oletussivu. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/2b2cbb69-bdc3-4403-84de-b6f2c510b09e)

Pysäytin apachen for now, korvasin testisivun komennolla "echo 'moi' | sudo tee /var/www/html/index.html"

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/adb66626-bebd-4799-ac98-f2008900d9b6)

Reboottasin demonin seuraavaksi.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/542f69dc-b7da-4866-bd88-93b95f6b8452)

Nyt Saltilla. Muutin topfilestä ajettavan komennon nimeksi apache.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/ba596337-d2de-44bf-9292-7220b9bf9153)

Kokeillaampas tällä init.sls -tiedostolla. Tuli seuraava virhe: 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/a0ad19b6-e863-40c0-a012-812e21147c4c)

Kokeillaampas Saltin docseista hieman muutetulla init.sls -tiedostolla apachen asennusta. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/5fab53af-c30b-45da-b22e-478653235478)

Sama virhe vieläkin. Kokeillaan googlata. Vaihdoin Top filestä sen apachen takaisin helloksi, ja nyt antaa vain syntax erroria. Vaikuttaa liittyvän siihen nimeen jotenkin. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/67978165-e1bc-4e8f-8aeb-c79591e141c0)

Muokkailin hieman init.sls:ää, ja tällä configilla sain sen toimimaan.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/7541c680-9534-4eb7-acaa-b63ce987aed4)

Ajoin komennon "sudo salt '*' state.apply", jolloin sain molemmilta orjilta tämän vastauksen.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/744905ee-d672-4ac4-a019-e288378e032c)

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/d9992df0-6876-4200-9638-ca90592a0d88)

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/5e6d4df9-04de-4058-ac67-40eec0389c8b)

Homma toimii!

## d) SSHouto

Avasin toisen virtuaalikoneeni, ja päivitin paketit. Asensin sshd:n komennolla sudo apt install openssh-server. Paketin nimi ei ollutkaan sshd, tämä piti googlata. 

Kävin ottamassa kommentin pois port-asetuksesta ja vaihdoin siihen 8888. Config-tiedosto on siis kansiossa /etc/ssh/

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/1bf63a14-d26d-4ce0-84b3-8304f1668405)

Reboottasin demonin komennolla "sudo systemctl restart sshd", ja katsoin statuksen komennolla "sudo systemctl status sshd". Kuvasta näkyy myös että portti on nyt 8888.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/768d22c1-cf07-47df-aebd-ad177e255be1)



## Lähteet:

https://terokarvinen.com/2023/configuration-management-2023-autumn/

https://github.com/laurijuusti/Linux-palvelimet/blob/main/Raportti5.md

https://salt-zh.readthedocs.io/en/latest/ref/states/all/salt.states.cmd.html

https://docs.saltproject.io/salt/user-guide/en/latest/topics/states.html#state-modules

