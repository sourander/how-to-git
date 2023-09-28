Ennen kuin voit käyttää gittiä versionhallintaan, sinun on **pakko** asettaa vähintään seuraavat kaksi (tietokoneen skoopissa) globaalia asetusta. Vaihdathan lainausmerkkien sisälle omat tietosi.

```bash
git config --global user.name "Etunimi Sukunimi"
git config --global user.email "etunimisukunimi@kamk.fi"
```

Tiedot tallentuvat globaaliin konfiguraatiotiedostoon kotikansiossasi. Tiedosto on `~/.gitconfig`.


## Konfiguraatioiden tarkistaminen

Lokaalit eli yhden git-repositorion sisäiset asetukset saa näkyville alla olevalla komennolla. Tämä komento kuuluu ajaa siis kansiossa, jossa sinulla on git-versionhallittu projekti, kuten vaikkapa `~/Code/sukunimi/amazingproject/`. Nämä löytyvät tiedostosta `<äskeinenkansio>/.git/config`

```bash
git config --local --list
```

Koko järjestelmätason oletukset, joiden pohjalta uuden projektin lokaali konfiguraatio muodostetaan, löytyy Windowsilla polusta `C:\Program Files\Git\etc\gitconfig`. Ne voi tulostaa seuraavalla komennolla:

```bash
 git config --system --list
```

Koko järjestelmätason omat asetukset, joita juuri äsken asetit kaksi (`user.name` ja `user.email`), löytyvät tiedostosta `~/config`, jossa aaltomerkki edustaa sinun kotikansiotasi (eli `C:\Users\username\`). Nämä voit tarkistaa komennolla:

```bash
git config --global --list
```





## Muut suositellut konfiguraatiot

Gittiä voi konfiguroida monin tavoin. Alla on esiteltynä muutama, äärimmäisen suositeltu konfiguraatio.



#### Rivinvaihdot

Aloitetaan rivivaihdoilla. Windowsissa rivinvaihto - eli enterin painaminen tekstitiedostoa muokatessa - kirjoittaa tiedostoon kaksi merkkiä: `CR` ja `LF`, jotka tunnetaan nimillä `Carriage Return` ja `Line Feed`. UNIX-pohjaisissa käyttöjärjestelmissä käytetään vain toista merkkiä eli `LF`.  Tämä usein on jo valmiiksi Git for Windows -asennuksessa oikein asetettuna.

```bash
# Windows
git config --global core.autocrlf true

# Linux tai macOS
git config --global core.autocrlf input
```

**TEHTÄVÄ:** Tarkista, että yllä oleva asetus on kunnossa. Git for Windows -asennus laittaa sen yleisesti oikeaan asentoon, mutta tarkista tuo, jotta opit käyttämään konfiguraatioon liittyviä komentoja.



#### Pullin strategia

Mikäli ajat komennon `git pull` tai `git pull origin main` ennen omaa `git push`-komentoa, aiheutat herkästi odottamattomia committeja. Lue lisää aiheesta täällä: [Why You Should Use git pull --ff-only | sffc's Tech Blog](https://blog.sffc.xyz/post/185195398930/why-you-should-use-git-pull-ff-only). Hyvä yleisvarma tapa ratkaista ongelma on asettaa seuraava konfiguraatio paikoilleen:

```bash
git config --global pull.ff only
```





#### Tekstieditori

Kun luot esimerkiksi git commitin komennolla `git commit`, aukeaa tekstieditori. Tämä editori on todella usein vakiona `vi` tai `vim`, mikä saattaa olla aloittelijan silmissä hankala työkalu. Voit vaihtaa sen huomattavasti helpompaan `nano`-nimiseen ohjelmaan näin:

```bash
git config --global core.editor "nano"
```


#### Oletushaaran eli branchin nimi

Git käyttää vakiona yhä `master`-nimistä (tarkista: `git config --system init.defaultBranch`) nimeä vakiohaaralle, joka luodaan kun teet kansiosta git-versionhallitun projektin käskyllä `git init`. Tämä on ongelmallinen kahdesta syystä:

1. **Inklusiivisuus**. Master-sanalla on huono historia.
2. **Käytännöllisyys**. GitHub, GitLab ja muut git-palvelua tuottavat yritykset ovat siirtyneet pitkälti `main`-nimeen. On käytänöllistä pitää heti alusta alkaen oma repositorio samankaltaisena kuin heidän oletuksensa.

Oletuksen voi vaihtaa seuraavalla komennolla:

```bash
git config --global init.defaultBranch main
```





