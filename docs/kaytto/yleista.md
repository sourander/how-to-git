# Yleistä

Tämä luku sisältää muutaman nyrkkisäännön gitin käytöstä, jotka on hyvä pitää mielessä.

## Dokumentoi kaikki mitä teet (✍️)

Tee `README.md` ja `LICENSE` ja lisäksi tarpeen mukaan jokin wiki/blogi/saitti/muu. Selitä, miksi projekti on olemassa, kuinka sen voi asentaa, kuinka sitä voi ajaa, mitä tekijänoikeuksia/lisenssejä siihen liittyy ja niin edelleen. Mikäli työskentelet jonkin uuden teknologian kanssa, on suositeltavaa luoda jopa `MEMO.md`, johon tallennat historian tekemisestä vaiheista. Tämä auttaa myöhemmässä käyttöönottovaiheessa tai vianselvityksessä merkittävästi.

!!! tip

    Mikset käyttäisi Github Pages -työkalua tehdäksesi itsellesi portfolio-tyylisen sivuston, jota voit käyttää esimerkiksi työnhaussa? Tämä sivu, jota luet nyt, on tehty Github Pagesilla. Koodi löytyy [gh:sourander/how-to-git](https://github.com/sourander/how-to-git) -repositoriosta. Sivusto päivittyy automaattisesti uuden pushin myötä (ks `.github/workflows/*.yml`).



## Älä laita suuria binääritiedostoja gittiin (💾)

Tutustu `.gitignore`-tiedostoon. Kyseessä on projektin juuressa, eli siis samassa hakemistossa missä on `.git/`-hakemisto, sijaitseva git-projektin konfiguraatiotiedosto. Tiedostossa listatut tiedostot ja hakemistot jätetään huomiotta gitin toimesta. Tämä tarkoittaa, että ne eivät näy `git status`-komennon tulosteessa, niitä ei voi lisätä `git add`-komennolla eikä niitä lähetetä etärepositorioon `git push`-komennolla. On luontevaa, että tiedostoon lisätään esimerkiksi seuraavat kohteet:

* `build/`-hakemisto, jos ohjelmasi tuottaa binääritiedostoja käännösvaiheessa
* `data/`-hakemisto, jos ohjelmasi käsittelee suuria datatiedostoja, joita ei ole tarkoitus versionhallita
* `*.log`, `*.tmp` ja muut väliaikaiset tiedostot, joita ohjelmasi tuottaa ajon aikana

Githubin [gh:github/gitignore](https://github.com/github/gitignore) reposta löytyy useille eri kielille esimerkkejä, joista voi katsoa esimerkkejä. Kenties parempi käytäntö on kuitenkin ajaa `git status -u` aina ennen `git add .` -komentoa ja tarkistaa, että mitään ylimääräistä ei ole tulossa mukaan. Jos on, muokkaa `.gitignore`-tiedostoa ja tarkista `git status -u` uudelleen, kunnes plörö on poissa.



## ... jos kuitenkin laitat binääritiedostoja gittiin (💾)

Joskus gitti osoittautuu ainoaksi sopivaksi tietyille tiedostoille, kuten dokumentaatioon tai testaamiseen liittyville tiedostoille. Opetuskäytössä GitLabiin voi sijoittaa myös koneoppimismallin koulutukseen käytettyä dataa – ainakin järjellisissä määrin. Tällöin on hyvä arvioida seuraavat vaihtoehdot:

* Jos tiedostoja on useita kymmeniä gigatavuja, sijoita ne muualle, kuten AWS S3:een tai Azure Blob Storageen, ja luo skripti, joka lataa datan tarvittaessa paikalliseksi.
* Jos tiedostojen koko on maksimissaan pari gigaa, käytä Git LFS:ää (Large File Storage), joka on suunniteltu erityisesti suurten tiedostojen hallintaan git-repositorioissa, ja meidän DC-labran GitLab tukee tätä ominaisuutta. Tähän löytyy helppo ohje [GitLab: Git LFS](lfs.md)-luvusta.

Jos olet epävarma, kysy kurssin opettajalta.


## Ymmärrä, älä muista (🧠)

Ethän aja git-komentoja `hauki on kala hauki on kala`-metodilla ulkoa muistellen, ymmärtämättä mitä ne tekevät. Gitin käyttö on hyvin dokumentoituna Githubin, Gitlabin ja muiden palveluiden sivuilla sekä ilmaisessa Pro Git -kirjassa sekä tällä sivustolla. Käytä ohjeita hyväksesi; lue niitä ajatuksella. Kun ymmärrät, muistitaakka vähenee.



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