# Avaimen luonti

## Luo avain

!!! warning

    Ennen kuin aloitat ohjeen seuraamisen, varmista, onko sinulla jo avain olemassa `~/.ssh/` hakemistossa. Jos sinulla on jo avain, älä luo uutta, vaan käytä sitä. Jos et tiedä, onko sinulla avainta, voit tarkistaa sen komennolla `ls ~/.ssh/`. Jos tiedostoja tai koko hakemistoa ei ole, voit jatkaa ohjeen seuraamista. Muutoin hyppää kohtaan [Lisää avain Git-palveluun](#lisaa-avain-git-palveluun).

Aloitetaan luomalla SSH-avain. Alla oleva komento toimii sekä Git Bashissä että macOS:n terminaalissa (zsh):

```sh
ssh-keygen -t ed25519 -C "jokin kommentti"
```

Suositeltu kommentti on muotoa `etunimi.sukunimi@kamk.fi kotikone`. Tämä tarkoittaa, että luot yhden ssh-avainparin per tietokone, jolla käytät gittiä. Mikäli luot virtuaalikoneen, luo sille oma avain. Mikäli ostat uuden koneen, luo sille oma avain.

**Ethän muokkaa tiedoston nimeä** kun `ssh-keygen` sitä kysyy, ellet tiedä mitä olet tekemässä. Paina ++enter++ kun tiedostonimeä kysytään. Kun hyväksyt komennon ehdottaman tiedostonimen, se luo kaksi tiedostoa hakemistoon: `~/.ssh/`. Aaltosulje viittaa käyttäjän kotihakemistoon.

* Julkinen avain: `id_ed25519.pub`
* Yksityinen avain: `id_ed25519`

!!! tip

    Tiedostolle on kannattavaa antaa ==passphrase==, jota ilman tiedosto on käyttökelvoton, varsinkin jos käytät yhteisessä käytössä olevaa tietokonetta. Tämä vaikeuttaa vääriin käsiin joutuneen avaimen käyttöä merkittävästi. Yllä oleva komento kysyy sitä; anna tai ole antamatta.


## Lisää avain Git-palveluun

### Vaihe 1: Kopioi leikepöydälle

Alla ohjeet julkisen avaimen kopioimiseksi leikepöydälle. Käy liittämässä se valitsemasi palvelun portaalissa.

=== "Windows (Git Bash)"

    ```sh
    $ cat ~/.ssh/id_ed25519.pub | clip
    ```

=== "macOS (Zsh)"

    ```sh
    $ cat ~/.ssh/id_ed25519.pub | pbcopy
    ```

=== "Ubuntu (Bash)"

    ```sh
    # Asenna ensin xclip jos ei löydy jo
    $ sudo apt update && sudo apt install xclip -y
    $ xclip -sel clip < ~/.ssh/id_ed25519.pub
    ```

### Vaihe 2: Lisää palveluun

Se, minne julkinen avain git-palvelussa lisätään tarkalleen, riippuu palvelusta. Lue palvelun omat ohjeet. Näitä ovat [Gitlab: Add an SSH key to your GitLab account](https://docs.gitlab.com/ee/user/ssh.html#add-an-ssh-key-to-your-gitlab-account) sekä [Github: Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?tool=webui). Jos käytät jotakin muuta palvelua kuin Github tai GitLab, lue kyseisen palvelun ohjeet.

!!! tip "TL;DR"

    Pikaohje GitLabiin on tässä: `Preferences` => `SSH Keys` => `Add new key` => ++ctrl+v++ kenttään `Key`.

### Vaihe 3: Testaa avain

Kun olet lisännyt avaimen käyttämäsi palvelun portaaliin, on hyvä varmistaa, että voit tunnistautua palveluun `SSH`:lla. Avainta käytetään jatkossa kaikkiin palveluihin kirjauduttuessa, mikäli se on ainut löytyvä ssh-avain. Avainta voi testata `repo.kamit.fi`-palvelun osalta näin:

=== "repo.kamit.fi"

    ```sh
    #         ┌─ Tässä pitää lukea SSH eikä HTTPS!!
    #         │
    #        ┌┴┐
    $ ssh -T ssh://git@repo.kamit.fi:45065
    ```

=== "Github"
    ```sh
    $ ssh -T git@github.com
    ```

Mikäli palvelu kysyy salasanaa (ei siis `passphrasea` vaan `password`:ia), ssh-avain ei ole syystä tai toisesta käytössä. Peruuta kirjautuminen painamalla ++ctrl+c++. Kokeile sulkea ja avata Git Bash terminaali uusiksi. Mikäli tämäkään ei auta, aloita vianselvitys. Jos ei ratkea järjellisessä ajassa, ==pyydä apua== kanssaopiskelijoilta tai opettajalta.

!!! note "Vianselvityksen aloitus"

    Tarkempaan vianselvitykseen voit ajaa yllä näkyvän ssh-komennon, mutta vaihda optioksi `-Tvvv`, jotta se tulostaa kaiken mahdollisen lokitukseen menevän rividatan. Lue se läpi huolella ja ala etsiä vikaa.

??? note "Mikä on fingerprint?"

    Kun käytät avainta ensimmäisen kerran, ssh client pyytää sinua varmistamaan, että palvelimen fingerprint on oikein.

    ```
    Cloning into 'test'...
    The authenticity of host '[repo.kamit.fi]:45065 ([212.116.36.9]:45065)' can't be established.
    ED25519 key fingerprint is SHA256:cL3YVM/KHB14av6S6YfY+ZnEH9tiaOhIQxfd3WUizNE.
    This key is not known by any other names
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```

    Mikäli kirjoitat `yes` ja painat enteriä, niin kyseistä hostia varten lisätään rivit tiedostoon `.ssh/known_hosts`. Mikäli poistat tuon tiedoston, varmistus tehdään seuraavan git-operaation kohdalla uusiksi.

Kun olet luonut ja testannut avaimen (`ssh -T <url>`-komennolla), voit alkaa käyttää gittiä kyseisen git servicen kanssa. Voit jatkaa esimerkiksi [Soolokäyttäjän ohjeeseen](../../kaytto/soolokayttaja.md).