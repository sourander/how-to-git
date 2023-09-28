Aloitetaan luomalla SSH-avain. Alla oleva komento toimii sekä Git Bashissä että macOS:n terminaalissa (zsh):

```sh
ssh-keygen -t ed25519 -C "jokin kommentti"
```

Suositeltu kommentti on muotoa `etunimi.sukunimi@kamk.fi kotikone`. Tämä tarkoittaa, että luot yhden ssh-avainparin per tietokone, jolla käytät gittiä. Mikäli luot virtuaalikoneen, luo sille oma avain. Mikäli ostat uuden koneen, luo sille oma avain.

**Ethän muokkaa tiedoston nimeä** kun `ssh-keygen` sitä kysyy, ellet tiedä mitä olet tekemässä. Paina ++enter++ kun tiedostonimeä kysytään. Kun hyväksyt komennon ehdottaman tiedostonimen, se luo kaksi tiedostoa hakemistoon: `~/.ssh/`. Aaltosulje viittaa käyttäjän kotihakemistoon.

* Julkinen avain: `id_ed25519.pub`
* Yksityinen avain: `id_ed25519`

Tiedostolle on kannattavaa antaa passphrase, jota ilman tiedosto on käyttökelvoton, varsinkin jos käytät yhteisessä käytössä olevaa tietokonetta. Tämä vaikeuttaa vääriin käsiin joutuneen avaimen käyttöä merkittävästi. Yllä oleva komento kysyy sitä; anna tai ole antamatta.


## Lisää avain Git-palveluun

Se, minne julkinen avain git-palvelussa lisätään, riippuu palvelusta. Lue palvelun omat ohjeet:

* [Gitlab: Add an SSH key to your GitLab account](https://docs.gitlab.com/ee/user/ssh.html#add-an-ssh-key-to-your-gitlab-account)
* [Github: Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?tool=webui)


```sh
# WINDOWS ONLY
cat ~/.ssh/id_ed25519.pub | clip

# macOS ONLY
tr -d '\n' < ~/.ssh/id_ed25519.pub | pbcopy

# UBUNTU ONLY
sudo apt install xclip
xclip -sel clip < ~/.ssh/id_ed25519.pub
```


## Testaa avain

Avainta käytetään jatkossa kaikkiin palveluihin kirjauduttuessa, mikäli se on ainut löytyvä ssh-avain. Avainta voi testata näin:

```sh
# Kamit Repo
ssh -T ssh://git@repo.kamit.fi:45065
```

Mikäli palvelu kysyy salasanaa (ei siis `passphrasea` vaan `password`:ia), ssh-avain ei ole syystä tai toisesta käytössä. Ajoithan aiemmin mainitut `eval` ja `ssh-add` komennot, mikäli olet kopioinut ssh-avaimen toiselta tietokoneelta? Kokeile sulkea ja avata Git Bash terminaali uusiksi.

Tarkempaan vianselvitykseen voit ajaa yllä näkyvän ssh-komennon, mutta vaihda optioksi `-Tvvv`, jotta se tulostaa kaiken mahdollisen lokitukseen menevän rividatan. Lue se läpi huolella ja ala etsiä vikaa.



## Käytä avainta

Huomaathan, että URI:n on oltava jatkossa muotoa, joka alkaa `ssh://...`, kuten:

```sh
# Tee näin.
git clone ssh://git@repo.kamit.fi:<port>/<user-or-group-name>/<repo-project-name>.git

# Älä tee näin. Tämä yrittää tunnistautua Git Credential Manager Coren popupilla
git clone https://repo.kamit.fi/janisou1/test.git
```

Repo Kamit käyttää custom TCP-porttia, joten URL:n osatekijät ovat:

```txt
      user        host
     ┌─┴─┐┌────────┴──────────┐
ssh://git@repo.kamit.fi:<port>/<user-or-group-name>/<repo-project-name>.git
└─┬──┘                        └────────────────────┬──────────────────────┘
scheme                                            path
```

Kun käytät avainta ensimmäisen kerran, ssh client pyytää sinua varmistamaan, että palvelimen fingerprint on oikein.

```
Cloning into 'test'...
The authenticity of host '[repo.kamit.fi]:45065 ([212.116.36.9]:45065)' can't be established.
ED25519 key fingerprint is SHA256:cL3YVM/KHB14av6S6YfY+ZnEH9tiaOhIQxfd3WUizNE.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Mikäli kirjoitat `yes` ja painat enteriä, niin kyseistä hostia varten lisätään rivit tiedostoon `.ssh/known_hosts`. Mikäli poistat tuon tiedoston, varmistust tehdään seuraavan git-operaation kohdalla uusiksi.



## Usean SSH-avaimen käyttö

Mikäli haluat luoda eri avaimet eri palveluja varten, tarvitset konfiguraatiotiedoston `~/.ssh/config`, jonka sisältö on esimerkiksi:

```sh
Host github.com
  IdentityFile ~/.ssh/github
Host example.com
  IdentityFile ~/.ssh/example
Host short_alias
  HostName some.very.long.aws.instance.name.amazonaws.com/
  User ec2-user
  Port 22
  IdentityFile ~/.ssh/something
```

Huomaathan, että useimmissa tilanteissa yhden avainparin pitäisi riittää per tietokone. Mikäli kuitenkin haluat käyttää yhtä avainta kaikilla käyttämilläsi tietokoneilla, sinun pitää keksiä jokin tietoturvallinen tapa siirtää yksityinen avain tietokoneelta toiselta. Tässä voi auttaa salasananhallintapalvelu kuten Lastpass. Yleisesti helpointa on kuitenkin luoda jokaiselle käyttämällesi tietokoneelle (ja virtuaalikoneelle) yksi avainpari, ja levittää tämän avainparin julkinen avain kaikkiin käyttämiisi palveluihin (Kamit Gitlab, Gitlab Cloud, DC Labran Gitlab, Github, Puhti supertietokone, eri palvelimet ja niin edelleen...)