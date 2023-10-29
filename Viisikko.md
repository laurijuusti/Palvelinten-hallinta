# Raportti 1, Viisikko (Sunnuntai 29.10.2023)

### OS: Windows 10 22H2
### Virtualisointi: VMWare Workstation 17 Player
### Host-tietokone: AMD Ryzen 7 3700x, 32GB RAM, NVIDIA RTX 3080
### VM: 2 CPU, 8GB RAM


## x) Lue ja tiivistä (klo. 20.26)

 - Ensimmäisessä artikkelissa näytettiin miten luodaan repositorio GitHubiin, ja sinne tiedostoja ja tekstiä.
 - Toisessa artikkelissa näytettiin salt-daemonin asennus, ja erilaisia komentoja sille.


## a) Saltin asennus 

Päivitin paketit, ja asensin saltin komennoilla

    $ sudo apt-get update
    $ sudo apt-get -y install salt-minion

Toisen komennon lopputulos:

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/c54816b9-b77b-4f05-b229-36221644fd67)

Version tarkastaminen:

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/d03ae9ca-24ab-44ee-bdef-33e9167e1913)

## b) Tilafunktiot

### 1. pkg.installed 

Kertoo onko koneelle asennettu spesifioidut paketit ja asentaa ne. Removed tekee saman mutta poistaa. Näyttää lopuksi muutokset.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/70fd3aa8-5635-4091-9296-2d92a59ff09c)

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/36765bae-e3a4-4fd0-a93e-dde96b270f5b)

### 2. File

Tiedostojen ja hakemistojen luonti onnistuu...

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/beec7939-94b6-49e9-bfe7-a088ddfebaa1)

...sekä niihin kirjoittaminen

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/7f7fcbcc-55a2-4a48-9fa3-4d2c55c4d869)

...ja niiden poistaminen 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/027e5b35-ddb6-4398-b8b1-6162bece9480)

### 3. Services

  Apachen käynnistäminen ja sammuttaminen onnistuu, toimii samalla tavalla kaikille prosesseille:
  
  ![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/409dbdec-d4e7-4138-afaf-f78bf9c17661)

  ![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/92b8f900-6ebc-42c1-8411-e763f9429281)

### 5. Users

Käyttäjien tietojen tarkistus onnistuu: 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/35f7fe66-2dce-41ef-ba0c-573cede079f5)

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/660d3bdc-47ec-40e9-b62c-fb6557c1ce2e)

Antaa true/false vastauksen. 

6. Komentojen ajo

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/b3ac1774-4bd8-4666-8c1d-ee7698ccf076)

## c) Indempotentti 

Indempotenssi tarkoittaa että jonkin komennon ajaminen monta kertaa tuottaa saman tuloksen kuin sen kerran ajaminen. Jos kokeilee käynnistää apachen kahdesti, niin toinen komento kertoo vain tiedon että se on jo käynnissä, ei yritä käynnistää uudestaan.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/db341d7c-c8d9-4b8a-83b1-9293fad65a90)

## d) Tietoja

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/ffb49388-323f-4e8e-a152-6a069426407c)

Kertoo lisätietoa kernelistä, käyttöjärjestelmästä ja virtualisoinnista. 

## Tiivistelmä, lähteet (klo. 21.11)

Raportissa leikin hieman saltilla ja sen eri komennoilla. Tiivistin myös tehtävänannon alussa olleet artikkelit.

Lähteet:

https://terokarvinen.com/2023/configuration-management-2023-autumn/#h1-viisikko

https://terokarvinen.com/2021/salt-run-command-locally/

https://terokarvinen.com/2023/create-a-web-page-using-github/

https://docs.saltproject.io/en/latest/topics/grains/index.html





