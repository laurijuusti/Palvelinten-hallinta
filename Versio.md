# Raportti 3, Versio (Perjantai 10.11.2023)

### OS: Windows 10 22H2 64-bit
### Kone: Ryzen 7 3700x, NVIDIA RTX 3080, 32GB DDR4 RAM


## a) Online

Menin selaimella github.com, loin uuden repositorion painamalla 'New'-painiketta sivuston etusivulla (olin jo valmiiksi kirjautunut), annoin sille nimen, kuvauksen, lisenssitiedot, ja tein README-tiedoston. Painoin 'Create Repository', jolloin sivu vei minut juuri tekemäni repon etusivulle. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/52c83c31-8675-40c0-bc2c-fb2c27cfb944)

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/b5762cee-fdd9-458e-9827-78e6c721eaf3)


## b) Dolly

Teen tätä windowsilla, joten avaan Powershellin painamalla Windows + X ja valitsemalla Powershell. Komennolla "git --version" tarkistan onko Git asennettuna, ja onhan se. Voimme jatkaa. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/371b1389-7bcf-48cf-a59a-488dad72a457)

Seuraavaksi navigoin komennolla "cd" kansioon jonne halusin repositorion tiedostot, ja kloonasin ne sinne komennolla "git clone https://github.com/laurijuusti/winter-test.git". Navigoin vielä komennon luomaan kansioon, ja siellähän ne oli kun katsoi kansion sisällön komennolla "dir".

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/91a59b86-74cf-432b-86eb-ccf3e575371a)

Loin kansioon Explorerin kautta uuden tekstitiedoston, ja lisäsin sinne hieman testitekstiä. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/1786b489-ad1b-45ce-b1d4-b09aee420bab)

Ajoin komennot "git add .", "git pull", "git commit" ja "git push", jolloin kävi näin. Eihän minulla tietenkään ollut SSH-yhteyttä repoon, eikä se anna päivittää sinne mitään. Korjataanpas tämä SSH:llä.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/9bb8718a-e488-4f07-9a2b-5e38ff6ef63a)

Generoin ssh-avaimet komennolla "ssh-keygen", lisäsin sen githubiin (klikkasin profiilikuvaa -> Settings -> SSH and GPG keys -> lisäsin sinne ja painoin "Add SSH key".

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/b3b1721f-6be9-446b-8df8-fa500038fef7)

Kokeillaampa pushaamista uudelleen. Ei toiminut senkään jälkeen (unohdin screenshotin), antoi saman 403 errorin. Kokeilin kloonata repon ssh:llä, lisäsin saman tekstitiedoston sinne ja kokeilin uudestaan. Piti vain spesifioida commit messagen editoriksi notepad komennolla "git config core.editor notepad", se jostain syystä defaulttasi VSCodeen jota koneellani ei enää ole. Vihdoinkin pushaaminen onnistui. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/a2773f81-1b96-454d-8ff8-7a27846dbc70)

Näkyy myös netissä!

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/529f7298-87ac-4836-aa55-973513fb967f)


## c) Doh!

Loin kansioon tyhmän muutoksen eli toisen tekstitiedoston.

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/9ff4bfd6-bb97-4ab8-8069-604491d4ce5e)

Kesken committia tajusin, että tätä ei saa committaa ja ajoin komennon "git reset --hard".

Tämä on lopputulos: 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/408cbf5c-7a92-4f8f-9fad-7748ed26c8b4)

Googlailun jälkeen en ollut vielä tähän tyytyväinen, koska tuossa mainittiin vielä tuo salainen.txt. Ajoin komennon "git reset --soft HEAD~1", joka poistaa viimeisimmän commitin ennen pushia ja nyt kun ajaa "git status", kaikki näyttää hyvältä. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/37ba7ed4-443f-4a2d-ab6f-f18a19352d70)

## d) Tukki

Komennolla "git log", saa lokin näkymään. 

![kuva](https://github.com/laurijuusti/Palvelinten-hallinta/assets/122888655/fa197bd2-efdc-4d8c-aa2a-f0f0b5ce881c)

Siellä näkyy tuo initial commit ja muut commitit, kuka sen on tehnyt ja milloin (github käyttäjänimi, tarkka aika ja vielä mitä tehtiin commit IDn kera. (commit message)

## Lähteet:

https://terokarvinen.com/2023/configuration-management-2023-autumn/

https://stackoverflow.com/questions/1611215/remove-a-git-commit-which-has-not-been-pushed

https://stackoverflow.com/questions/10564/how-can-i-set-up-an-editor-to-work-with-git-on-windows





