# Miniprojekti (Lauantai 9.12.2023)

### OS: Windows 10 22H2 64-bit
### Kone: AMD Ryzen 7 3700x, 32GB RAM, RTX 3080
  
## Miniprojekti

Loin itselleni ensin testiympäristön kahdesta Debian 11 virtuaalikoneesta käyttäen Vagrantia ja Tero Karvisen luomaa vagrantfileä, jonka muokkasin luomaan herran ja yhden orjan. Sain tämän toiminaan komennoilla      

    $ vagrant init debian/bullseye64, vagrant up

Vagrantfile asentaa orjalle valmiiksi paketin "salt-minion".

Vagrantfilen sisältö:

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/b1c48bc9-993f-48f0-bb57-a1126a3d93de)

SSH:tin itseni masterille, hyväksyin avaimet sekä testasin että herra-orja arkkitehtuuri on pystyssä. 

    $ vagrant ssh tmaster, sudo salt-key -A, sudo salt '*' test.ping
    
![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/8f5a8f75-fc29-4bbf-b907-c73d279c77bc)

Miniprojektini tarkoitus on nyt saada pelille Unturned serveri pystyyn käyttäen LinuxGSM:ää. Tähän tarvitaan SteamCMD.

Lisään tiedostoon /etc/apt/sources.list ensimmäisen ja toisen rivin jälkeen kohdan "contrib non-free", joka lisää paketinhallintaan Debianin Non-free paketit, joista esim. SteamCMD löytyy. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/098587fc-c405-417b-8d55-6b5db8da6452)

Seuraavaksi ajan komennon "sudo dpkg --add-architecture i386", joka sallii Multi-Archin. Tämän jälkeen päivitin paketit "sudo apt update", "sudo apt upgrade".

Tämän jälkeen asensin Steamin ja SteamCMD:n. "sudo apt install steam" "sudo apt install steamcmd". Sitten asensin tarvittavat riippuvuudet:

"sudo apt install curl wget file tar bzip2 gzip unzip bsdmainutils python3 util-linux ca-certificates binutils bc jq tmux netcat lib32gcc-s1 lib32stdc++6"

Käytän LinuxGSM:n ohjeita serverin pyöräyttämiseen. https://linuxgsm.com/servers/untserver/

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/e1dde69b-e6c2-4db4-a0e4-138813a62b26)

Ajoin komennot, ja pääsin setuppiin. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/d74e8bef-971d-4a46-9ee1-6adf04f06b43)

Tämän jälkeen asennus ei toiminut. Piti käydä ajamassa tuo "./untserver install" roottina jotta kaikki riippuvuudet asentuisi, anyway, nyt taas setupissa.

Setuppi ei vieläkään toiminut, herjasi appmanifesteista joidenka tiedän liittyvän jotenkin Steamiin. Otan helpon reitin, kokeilen toista peliä. Otan Call of Duty: World At Warin toiseksi peliksi.

Näitä ohjeita käyttäen installeri lähti toimimaan: 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/3cf73340-6325-4f7d-a5b4-118ce778dc63)

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/5df7804e-dd49-4296-a12d-3956ac6f6588) 

Asennus on todella hidas, kesti noin 15 min.

Asennus valmis! Komennolla "./codwawserver start" serveri käynnistyy.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/21d01410-fbc3-471f-b00f-6dcd8d74daaa)

Jaahas. Eipä käynnistynytkään. Kokeilin vielä debugata "./codwawserver debug", mutta tuloksetta. Jätän tällä kertaa tähän ja menen nukkumaan.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/8bff6b18-2348-43a6-a7c9-a19e568cc397)

Kävin asettamassa koneille Virtualboxin asetuksista lisää muistia, jos se toimisi.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/8f399078-be91-4779-8ba8-ce3477ae321b)

Hei, nyt serveri näyttäisi olevan päällä! Pääsin yhdistämäänkin peliin käyttämällä pelin sisäistä konsolia "§" näppäimestä komennolla "/connect 192.168.12.3:28960"

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/ecd4d64d-dccd-4c3e-bfc6-367562fd10a8)

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/65149225-783c-4916-94a7-f2ef149f9ec4)

Kokeillaan automatisoida prosessia saltilla. Tein kansioon /srv/salt/paketit tiedoston init.sls, jossa on listattuna kaikki tarvittavat riippuvuudet. Koitin ajaa tilan "sudo salt '*' state.apply paketit", mutta sain erroria ettei steamcmd:tä löyty. No sehän johtuu siitä että se on Debianin non-free paketeissa. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/9560df66-c6cb-428c-9d64-873d39da66aa)

Kopioin masterin src/salt/ kansioon sources.list tiedoston jossa on tarvittavat muokkaukset non-free pakettien lataamiseen. Teen tilan, jolla tämä tiedosto menee orjille myös oikeaan paikkaan. Tässä init.sls:n sisältö:

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/e09d583d-0367-4cba-ae70-70e7d0b24c72)

Kokeillaan tilaa. "sudo salt '*' state.apply pakettilähteet"

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/07db000e-ecc5-4d49-98ac-b2e84843b7d0)

Kokeillaan ajaa paketit sisään. "sudo salt '*' state.apply paketit"

Vieläkin vähän ongelmaa steamcmd:n kanssa. Ehkä koska en päivittänyt paketteja? Muokataampa tilaa hieman. Lisäsin sinne kohdan, jonka pitäisi päivittää paketit. Ei toiminut vieläkään, edelleen "package steamcmd has no installation candidate".

Unohdin lisätä sinne tuon "dpkg --add-architecture i386" -komennon. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/124c2ed5-be38-48e4-b316-33c0daf18524)

Nyt komento ajoi, mutta sain erroria "Sub-process /usr/bin/dpkg returned an error code (1)."

Kokeilin poistaa steamcmd:n init.sls:stä, ja muiden riippuvuuksien asennus sujui ongelmitta.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/22e22a88-c0df-42ec-9300-8d1e1f23e652)

Kokeilin testausmielessä asentaa steamcmd:n käsin, "sudo salt '*' cmd.run 'sudo apt install steamcmd', ja kävi näin:

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/c5479bb7-3617-4f06-b5fa-48424454f3d6)

Tähän jäi tällä kertaa.

## Tiivistelmä, lähteet

Raportissa kokeilin luoda peliserverin, ja automatisoida sen Saltilla orjille. Tämä ei kuitenkaan onnistunut täydellisesti. 

Lähteet:

https://terokarvinen.com/2023/configuration-management-2023-autumn/

https://terokarvinen.com/2023/salt-vagrant/

https://linuxhint.com/enable-non-free-packages-debian-11/

https://wiki.debian.org/Steam

https://linuxgsm.com/servers/untserver/

https://docs.linuxgsm.com/commands/debug

https://docs.linuxgsm.com/troubleshooting

https://docs.saltproject.io/en/latest/ref/states/all/salt.states.pkg.html

https://linuxgsm.com/servers/codwawserver/

https://stackoverflow.com/questions/51023815/upgrade-all-packages-in-a-minion-using-state
