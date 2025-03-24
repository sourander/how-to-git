# Gitlab: Ryhmäkäytön ohje

!!! warning

    Git:n opiskelu ottaa aikansa. On suositeltavaa pyörittää henkilökohtaisia repositorioita ensin. Kannattaa aloittaa soolokäyttäjän ohjeella esimerkiksi siten, että kirjoitat oppimispäiväkirjat Markdown-muodossa ja commitoit muutokset GitLabiin.

Jos sinulla ja ryhmäläisilläsi on tarve versionhallita jotakin koodia yhteisesti, tarvitsette:

* Repositorion, johon kaikilla on oikeudet.
* Yhteiset pelisäännöt ja käytännöt.
    * ...joihin lukeutuu se, että `main`-branchiin ei pusketa mitään!
    * Featureita tai bugeja edustavat ==branchit==.
    * Jokaista branchia varten löytyy oma ==Issue==.
* Kärsivällisyyttä.

Kunhan nämä ovat kunnossa, niin olette valmiita astumaan ketterän ohjelmistonkehityksen ja DevOpsin taikamaailmaan! :mage:

## Video-ohjeistus

Alla on videomuotoinen 4-osainen ohje, jossa esitetään, kuinka kuvitteelliset henkilöt Jack ja Rose hallitsevat yhteiskäyttöistä repositoriota.

Videoissa:

- [x] Aloitetaan täysin tyhjästä repositoriosta
- [x] Luodaan main branch
- [x] Luodaan kaksi issueta
    * Jack työskentelee yhden parissa
    * Rose työskentelee toisen parissa
- [x] Jack suorittaa Pull Requestin (Merge Request)
- [x] Rose yrittää suorittaa ==konfliktoivan== Pull Requestin
- [x] Rose korjaa konfliktin
    * Merge `main` => `<rosen-branch>`.
- [x] Rose suorittaa korjatun Pull Requestin.

### Osa 1/4

<iframe width="560" height="315" src="https://www.youtube.com/embed/q5jBQPxF5co?si=_QcnP7jALNacmLqV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

**Video 1:** *Videossa luodaan Gitlab-projekti, ja sille luodaan projektihakemistot kahden virtuaalikäyttäjän (Jack ja Rose) kansioihin.*

### Osa 2/4

<iframe width="560" height="315" src="https://www.youtube.com/embed/eElYQnIodMc?si=b8gRKtPSCp3lPDHj" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

**Video 2:** *Videossa luo kaksi Issueta (yksi Issue ja yksi Bug), ja kummankin näiden pohjalta yksi branch.*

### Osa 3/4

<iframe width="560" height="315" src="https://www.youtube.com/embed/yXn8wR0RZco?si=U4bFO86vMMu8UGqC" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

**Video 3:** *Videossa tehdään bugfix, joka pusketaan Gitlabiin ja siitä tehdään Merge Request (ja merge). Tämä toimii pohjana seuraavan videon konfliktille.*

### Osa 4/4

<iframe width="560" height="315" src="https://www.youtube.com/embed/jL5mtRrESmc?si=wTdUpbmA4VdFwSqY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

**Video 4:** *Videossa luodaan feature commit ja merge request. Merge request vaatii konfliktit ratkaisua.*