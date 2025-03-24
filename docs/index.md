# Aloita tästä

!!! warning
    For now, this repository contains only Finnish guides, but it may be translated into English in future.

Tämä dokumentaatio sisältää ohjeistukset siihen, kuinka käyttää Gittiä opiskelijana. Kurssin esimerkit perustuvat pitkälti Kamitin ylläpitämään Gitlabiin, mutta samat ohjeet on sovellettavissa Githubiin, Gitlab Cloudiin, muissa organisaatioissa hostattuihin on-prem Gitlab-asennuksiin, Azure DevOpsiin ja niin edelleen. Dokumentaatio on suunniteltu luettavaksi järjestyksessä alusta loppuun: avaa vasemmalla näkyvää navigaatiota ja klikkaa linkit läpi järjestyksessä.

## Mikä on git?

Itse `git` on Linus Torvaldsin kehittämä versionhallintatyökalu: aiemmin mainitut yritykset tuottavat "git hosting serviceä". Niissä kaikissa toimii siis sama `git` konepellin alla, mutta kukin niistä tarjoaa muita palveluita sen päällä. Ihan vähimmillään ne tarjoavat tunnistautumisen ja jonkin sortin online-portaalin, mutta palveluihin kuuluu myös muun muassa vuokrattavaa pilvirautaa, jolla voi suorittaa koodin testausta. 

!!! tip
    Tämä sivusto hyödyntää Githubin palvelua nimeltään Github Pages, joka luo Github-projektille julkisesti saatavilla olevan dokumentaation.

Tämän materiaalin syventävänä ja tukevana materiaalina kannattaa lukea muuta dokumentaatio ja/tai kirjallisuutta. Yksi äärimmäisen suositeltu lähde on [Ilmainen Pro Git PDF-kirja](https://git-scm.com/book/en/v2). Joihinkin pattitilanteisiin löytyy näppäriä ratkaisuita myös [Oh Shit, Git?!?](https://ohshitgit.com/)-sivustolta.

![Git versionhallinta](images/dalle_git_terracotta.jpg)

**Kuvio 1:** *DALL-E 3:n näkemys versionhallinnasta.*

## Mikä git ei ole

Näin *Web 2.0* -aikakaudella on hyvä korostaa, että: 

* ==git ei ole suuryhtiön online-palvelu==, kuten vaikkapa OneDrive, Spotify tai Instagram. 
* Git ei tarjoa suoraan tiedostojen varmuuskopiointia tai synkronointia useiden laitteiden välillä kuten OneDrive, Google Drive tai Dropbox. 
* Git:iä ei lähtökohtaisesti käytetä selaimella.

Vaikka git ei ole pilvipohjainen palvelu, se voi toimia yhdessä sellaisten palveluiden kanssa, kuten Github, Gitlab tai Bitbucket, jotka tarjoavat keskitettyjä säilytyspaikkoja gitiin perustuville projekteille. Näiden palveluiden kautta voidaan jakaa koodia, tehdä tiimityötä ja jopa integroida jatkuva testaus ja käyttöönotto. Huomaa, että konepellin alla toimii silti ihan tavallinen git. Esimerkiksi Gitlab:lla on heidän palveluissaan ajettu `git init`-komento (joskin `--bare` optionilla.)

## Git ei ole ainoa

Git on vain yksi versionhallintatyökalu monien joukossa. On olemassa muitakin työkaluja, kuten Subversion (SVN) ja Perforce. Git on kuitenkin noussut suosituimmaksi työkaluksi avoimen lähdekoodin projekteissa.

## Antaa enemmän kuin ottaa

Git ei ole aluksi helppo käyttää, mutta oikein käytettynä se antaa enemmän kuin ottaa. Varmista, että otat git:n käytön haltuun opintojesi aikana: käytä sitä niin usein kuin mahdollista. Jos teet projektia, käytä versionhallintaa. Jos ei ole vahvoja syitä käyttää jotakin muuta versionhallintatyökalua, käytä git:iä.
