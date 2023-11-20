
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



## b) Top



## c) Apache



## d) SSHouto



## Lähteet:

https://terokarvinen.com/2023/configuration-management-2023-autumn/





