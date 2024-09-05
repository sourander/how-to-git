## Yleiset komennot

Tässä dokumentissa esitellään hyvin tiivis lista yleisimmistä git-komennoista. Kattavamman, mutta silti yhä helppolukuisen listan, löydät PDF-muodossa [Github: Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf).

Git-komentojen opiskeluun voit hyödyntää myös valmiita roadmappeja, kuten [Roadmap.sh: Learn Git and Github](https://roadmap.sh/git-github). KAMK-ympäristössä voit korvata Github-moduulit Gitlab:n vastaavilla opeilla; samoilla hakusanoilla löytyy Gitlabin dokumentaatiota.

Alussa kannattaa kuitenkin keskittyä peruskäyttöön. Tässä on listattu yleisimmät komennot, joita tarvitset päivittäisessä työskentelyssä jo opintojen alkuvaiheessa.

### Aloitus

Tyypillisesti aloitat työskentelyn valitsemalla näistä toisen:

1. `git init`: Luo uuden git-repositorion eli `.git/` hakemiston.
2. `git clone <url>`: Kloonaa olemassaoleva git-repositorio.

Yksinkertaisempaa on aloittaa Gitlabissa uusi projekti ja kloonata se lokaalisti eli vaihtoehto 2.

### Aja näitä usein

* `git status -u`: Näyttää repositorioon liittyvät muutokset.
* `git log --oneline`: Näyttää commit-historian yhdellä rivillä per commit.

### Stage

* `git add <file>`: Lisää tiedosto gitin seurantaan. Jos tiedostoksi on valittu `.` tai `--all`, lisätään kaikki muuttuneet tiedostot.
* `git add .`: Lisää kaikki uudet tiedostot ja muutokset projektisi syövereistä stagingille. Aja ehdottomasti `git status` ennen tätä komentoa ja varmista, ettei mukana ole esimerkiksi binääritiedostoja, cache-tiedostoja tai muuta plöröä.

### Commit

* `git commit -m "message"`: Tallentaa muutokset commitiksi. `-m`-flagiin voi kirjoittaa commit-viestin.

### Lokaali --> Remote

* `git push`: Lähettää nykyisen branchin lokaalit commitin remote-repositorioon.

### Lokaali <-- Remote

!!! note

    Alla olevissa komennoissa oletetaan, että olet asettanut `pull.ff=only`-asetuksen. Jos olet epävarma, käy lukemassa [Asennus/Konfiguraatio](asennus/konfiguraatio.md)-luvusta ohje.

* `git pull`: Hakee muutokset remote-repositoriosta ja yhdistää ne lokaaleihin muutoksiin. Jos tämä antaa varoituksen, olet todennäköisesti kohdannut konfliktin. Käytä alla olevaa komentoa.
* `git pull --no-ff`: Ohittaa `pull.ff=only`-asetuksen eli pakottaa mergen. Git lisää konfliktoiviin tiedostoihin rivejä, jotka osoittavat, mitä on muuttunut ja missä. Ratkaise konfliktit, lisää tiedostot stagingille, commitoi ja puske remoteen. Katso ohje [Käyttö/Gitlab: Ryhmäkäytönohje](kaytto/ryhmakayttaja.md)-luvusta.

Huomaa, että `git pull` on yhdistelmä komennoista `git fetch` ja `git merge`. `git fetch` hakee muutokset remote-repositoriosta ja `git merge` yhdistää ne lokaaleihin muutoksiin.

### Branch

Pienten sooloprojektien kanssa pärjäät pelkällä `main` branchilla. Kun tekijöitä on enemmän, branchit auttavat eri osa-alueiden erottamisessa ja yhdistämisessä.

* `git branch -v`: Näyttää branchit ja kertoo, missä branchissa olet.
* `git switch <branchname>`: Vaihtaa branchia.

!!! tip

    Voit luoda branchit Gitlabin web-käyttöliittymässä. Tällöin saat ne helposti kytkettyä Issueen, jonka ne ratkaisevat. Tähän löytyy video-ohje [Käyttö/Gitlab: Ryhmäkäytönohje](kaytto/ryhmakayttaja.md)-luvusta. 