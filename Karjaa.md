# Raportti 2, Karjaa (Saturday 4.11.2023)

### OS: Windows 10 22H2 64-bit
### Kone: i5-10300H, 8GB RAM

## x) Lue ja tiivistä (klo. 23.10)

 - Cattle-mindset servereissä on ikään kuin sama asia kuin karjaa, jos jokin palvelin kymmenistä tai sadoista menee alas tai rikki, se on nopeasti ja helposti korvattavissa.
 - Vagrantilla saa alle minuutissa virtuaalikoneen pystyyn johon saa SSH-yhteyden ja sen voi tuhota tarvittaessa.
 - Kolmannessa artikkelissa puhuttiin kuinka Vagrantilla saa automaattisesti luotua kolme konetta, hyväksyä "orjat", ajaa niillä komentoja ja lopuksi tuhota ne. 

## a) Vagrantin asennus

Latasin Vagrantin kotisivulta (https://developer.hashicorp.com/vagrant/downloads?product_intent=vagrant), käynnistin installerin, käynnistin koneen uudestaan ja asennus valmistui:

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/829bf97f-119e-4134-8f30-4252fd08ad7b)


## b) Yksi maankiertäjä

Navigoin työpöydälle Windowsin komentokehotteessa komennolla cd, ja ajoin komennon "vagrant init debian/bullseye64", joka loi Vagrantin config-tiedoston. Korvasin tiedoston sisällön Teron artikkelista löytyvällä slave-master tiedostolla, ja ajoin komennon "vagrant up", jolloin Vagrant lähti asentamaan kolmea virtuaalikonetta. 

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/1d9fa4d2-ea1d-4b66-8466-9130ac950688)

Netti ja ssh toimii! "ping google.com" sekä "vagrant ssh tmaster"

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/5a189abf-7388-4b7d-a7a0-1b6954ecb1f4)

## c) Oma orjansa

Tuli tehtyä jo tuossa b) kohdassa, asensin 2 orjaa ja herran samalla Vagrantfilellä. "vagrant up"

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/73bf4b57-a8bc-46e2-bf01-5fb94fc9449f)

## d) Herra-Orja

Hyväksyin orjien avaimet, ja testasin että verkko toimii pingaamalla orjat: "sudo salt-key -A" sekä "sudo salt '*' test.ping"

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/58b344e0-f388-4175-a1c6-5bb537b61c0f)

## e) Indempontti

Ajoin hieman state.single komentoja: 

1. "sudo salt '*' state.single pkg.installed neofetch"

   Neofetch asentui molempiin orjiin

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/cf4d5dca-b10e-4788-b651-c4bcc43e8aad)

Loin molempiin käyttäjän "lauri", komennolla "sudo salt '*' user.present lauri"... 

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/79f75626-6545-4eb2-a054-26d14aceb2aa)

Ja poistin käyttäjät "sudo salt '*' user.absent lauri".

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/e3e9da1e-3eca-4851-9a19-ff48b5529b98)

## f) Tekniset tiedot

Ajoin grains.items komennon "sudo salt '*' grains.items"orjille, antoi ihan liikaa tietoa molemmista orjista mikä ei näytölle mahdu: 

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/ee917176-8e8d-42ac-9626-e8648611ea83)

## g) Shell-komento

Shell-komento toimii, "sudo salt '*' cmd.run 'hostname -I'"

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/3305e28e-db27-4e87-a557-9b7c36868905)

## h) Hello, IaC
Loin kansion /srv/salt/hello komennolla "sudo mkdir -p /srv/salt/hello", tein tiedoston init.sls komennolla "sudoedit /srv/salt/hello/init.sls", johon kirjoitin sisällön

    /tmp/infra-as-code:
      file.managed

Ajoin komennon "sudo salt '*' state.apply hello", joka teki muutokset ja loi orjiin tiedoston /tmp/infra-as-code

   ![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/673e8af0-f098-439b-b62e-30593fc59d42)

SSH:tin orjaan sisään ja tarkistin todella, että hakemisto on luotu, ja siellähän se oli. 

![image](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/108ff0d0-1a46-4f03-9d15-aeee76592eb0)


## Tiivistelmä, lähteet (klo. 1.20)

Raportissa tiivistin artikkelit, asensin herra-koneen ja kaksi orjaa Vagrantilla, ja leikin niillä hieman verkon yli. 

Lähteet:

https://terokarvinen.com/2023/salt-vagrant/

https://terokarvinen.com/2023/configuration-management-2023-autumn/

https://tuomasvalkamo.com/CMS-course/week-6/

https://terokarvinen.com/2021/salt-run-command-locally/





