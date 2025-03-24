# Yleistä

Tämä luku sisältää muutaman nyrkkisäännön gitin käytöstä, jotka on hyvä pitää mielessä.

## Dokumentoi kaikki mitä teet (✍️)

Tee `README.md` ja `LICENSE` ja lisäksi tarpeen mukaan jokin wiki/blogi/saitti/muu. Selitä, miksi projekti on olemassa, kuinka sen voi asentaa, kuinka sitä voi ajaa, mitä tekijänoikeuksia/lisenssejä siihen liittyy ja niin edelleen. Mikäli työskentelet jonkin uuden teknologian kanssa, on suositeltavaa luoda jopa `MEMO.md`, johon tallennat historian tekemisestä vaiheista. Tämä auttaa myöhemmässä käyttöönottovaiheessa tai vianselvityksessä merkittävästi.

!!! tip

    Mikset käyttäisi Github Pages -työkalua tehdäksesi itsellesi portfolio-tyylisen sivuston, jota voit käyttää esimerkiksi työnhaussa? Tämä sivu, jota luet nyt, on tehty Github Pagesilla. Koodi löytyy [gh:sourander/how-to-git](https://github.com/sourander/how-to-git) -repositoriosta. Sivusto päivittyy automaattisesti uuden pushin myötä (ks `.github/workflows/*.yml`).



## Älä laita suuria binääritiedostoja gittiin (💾)

Tutustu `.gitignore`-tiedostoon. Kyseessä on projektin juuressa, eli siis samassa hakemistossa missä on `.git/`-hakemisto, sijaitseva git-projektin konfiguraatiotiedosto.

Githubin [github / gitignore](https://github.com/github/gitignore) reposta löytyy useille eri kielille esimerkkejä, joista voi katsoa esimerkkejä. Parempia tapa on kuinkin ajaa aina ennen `git add` -komentoa komento `git status -u`.



## ... jos kuitenkin laitat binääritiedostoja gittiin (💾)

Joskus gitti osoittautuu ainoaksi sopivaksi tietyille tiedostoille, kuten dokumentaatioon tai testaamiseen liittyville tiedostoille. Tämä voi olla OK-ratkaisu, olettaen että tiedostot eivät ole useiden gigatavujen kokoisia vaan mieluummin kilo- tai megatavuluokassa. Mikäli teet näin, luo tiedosto `.gitattributes`. Kyseinen konfiguraatiotiedosto mahdollistaa, että voit määrittää käsin, mitkä projektin tiedostot ovat binääriä.

```
*.obj binary
*.exe binary
*.dat binary
*.wav binary
```

Mikäli tiedostot ovat satojen megatavujen tai gigatavujen kokoisia, lisääthän mieluummin `README.md`-tiedostoon ohjeet, mistä ne voi ladata. Näppärä koodari voi jopa tehdä skriptitiedoston, joka lataa ne automaattisesti oikeaan lokaatioon esimerkiksi AWS S3:sta, Azure Blob Storagesta, CSC:n Allas-palvelusta tai vaikka OneDrive/Sharepointista.



## Ymmärrä, älä muista (🧠)

Ethän aja git-komentoja `hauki on kala hauki on kala`-metodilla ulkoa muistellen, ymmärtämättä mitä ne tekevät. Gitin käyttö on hyvin dokumentoituna Githubin, Gitlabin ja muiden palveluiden sivuilla sekä ilmaisessa Pro Git -kirjassa. Käytä niitä hyväksesi; lue niitä ajatuksella. Kun ymmärrät, muistitaakka vähenee.



## Tarkista muutokset ennen committia. (🔍)

Ethän koskaan aja komentoja `git add .` ja `git commit -m "jotain"` tarkistamatta, mihin tiedostoihin olet koskenut ja millä tavalla. Aluksi on hyvä tapa käyttää lokaalia testausta ennen `git push`-komentoa. 

!!! note

    Myöhemmin opit käyttämään CI/CD-palveluita, jotka testaavat koodisi automaattisesti ennen kuin se päätyy muiden käyttöön - tästä ei kannata murehtia aloittelijena.



## Kirjoita merkityksellisiä commit-viestejä (📖)

Commit edustaa muutosta koodissa, dokumentaatiossa tai muussa projektisi sisällössä. Commitin viestin tulisi kuvastaa, mikä on muuttunut. 

❌ `Added some code lol`

✅ `Added Save As funtionality to editor`



## Työskentele pienissä inkrementeissä (🔨)

Jos sinulle tulee fiilis, että commit message on proosaa, joka sisältää `...after which I ...`, ja `..and also...`, ja `...including but not limited to...`, ja `...and as a final step I refactored all code`, niin todennäköisesti työskentelet aivan liian suurissa paloissa. Hyvä git game loop on seuraava:

* Tee pieni muutos kerrallaan.
* Testaa se.
* Stage, Commit & Push.
* Repeat.



## Fetch tai Pull (🔁)

Jos et työskentele yksin projektin parissa, vaan joku muu tiimin jäsen voi lisätä/muokata saman branchin sisältöä, hyödynnä mieluiten brancheja - tai aja git pull aina ennen pushia. Branchien käyttö on neuvottu [GitLab: Ryhmäkäytön ohje](ryhmakayttaja.md)-luvussa.

Mikäli työskentelet yksin, aloita päivä `git pull`:lla ja lopeta `git push`:iin. Tämä on neuvottu [Gitlab: Sooloilihan ohje](soolokayttaja.md)-luvussa.



## Don't panic (🧘)

Jos saat virheilmoituksen tai git avaa jotakin sinulle vierasta, kuten `vim`-tekstieditorin, älä hätiköi ja copy-pastea jokaista StackOverFlow:sta löytämääsi koodirimpsua. Hengitä rauhassa, lue mahdolliset virheilmoitukset läpi huolella ja kysy tarpeen mukaan apua muilta.

!!! tip

    Huomaa, että saat tarkempia virheilmoituksia `verbose`-flagilla. Esimerkiksi `git pull --verbose` tai `git push -v`.