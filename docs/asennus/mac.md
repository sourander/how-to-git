## Käytä Z Shelliä

Z Shellin (`zsh`) pitäisi olla macOS:ssä nykyisin default, mutta voi myös olla, että Terminal käynnistää kilpailevan shellin eli `bash`:n. Mikäli näin on, macOS:n pitäisi neuvoa sinua ajamaan komento, joka näkyy alla. Aja komento ja käynnistä Terminal uusiksi.

```bash
$ chsh -s /bin/zsh
```

## Asenna Homebrew

Homebrew on vastaavanlainen paketinhallinta kuin Snap, Flatpak, Chocolatey tai jopa Ubuntusta tuttu ATP tai Red Hatistä tuttu DNF. Valitettavasti macOS:ssä ei ole valmiina omaa, joten avoimen lähdekoodin yhteisö on luonut puutteen tilalle Homebrew:n. Sitä käytetään asentamaan, päivittämään, hallinnoimaan ja poistamaan sovelluksia. Useimpia ohjelmistonkehitykseen tai shell-komentoihin liittyviä sovelluksia et löydä AppStoresta vaan ne tulee asentaa Homebrew:n tai vastaavan avulla. Jos haluat tarkat asennusohjeet, lue mac.install.guide-sivuston: [Install Homebrew Complete Guide](https://mac.install.guide/homebrew/3.html). Jos olet pelkkää asennuskomentoa vailla, aja [Homebrew:n kotisivuilta](https://brew.sh/) löytyvä komento:

```bash
# Homebrew:n asennuskomento on bashillä ajettava shell-skripti. Tämä komento lataa ja ajaa sen.
# Tuloste sisältää ohjeistusta ja tietoja asennuksesta. Lue se! Alla lyhennelmä:
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
==> This script will install:
/opt/homebrew/bin/brew
...
==> The following new directories will be created:
/opt/homebrew/bin
/opt/homebrew/etc
...
```

HUOM! Jos olet joskus ajanut komennon `xcode-select --install`, joka asentaa Linux-maailmasta tuttuja komentoriviltä ajettavia sovelluksia kuten `gcc` sekä `clang`. Mikäli et, Homebrew:n asennus käynnistää XCode Command Line Tools:n asennuksen. Homebrew tarvitsee näitä ohjelmia.

Lue asennuksen tarjoamat ohjeet tarkkaan. Asennus pyytää sinua lisäämään yhden rivin .zprofile-tiedostoon, joka voi olla tai voi olla olematta käytössä vakiona. Rivi näyttää muutoin samalta kuin alla oleva, mutta alla olevassa on mukana kommentti. Suosittelen pitämään `.zprofile` ja `.zshrc` tiedostot kommentoituina, jotta tiedät mitä mikäkin rivi tekee, ja miksi olet sen sinne lisännyt.

```bash
# .zprofile sisältö alla:

# Add Homebrew-related env variables
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Jatkossa ympäristömuuttujan `$PATH` pitäisi sisältää Homebrew:n asennuskansio. Voit tarkistaa tämän seuraavalla komennolla. Tulosteen pitäisi sisältää kansio `/opt/homebrew/bin` jos sinulla on ARM-sirullinen Apple. Vanhemmissa Intel-pohjaisissa koneissa asennuskansio on `/usr/local`. Asennuskansion pitäisi olla sinulle tuttu, mikäli luit aiempien komentojen tulosteen.

```bash
$ echo $PATH | tr ":" "\n"
/opt/homebrew/bin
/opt/homebrew/sbin
/usr/local/bin
...
```

## Asenna git

Python-koodi kannattaa pistää lähes poikkeuksetta gittiin, ja tämä on usein myös eri kursseilla tehtävänantojen oletus. Xcode:n mukana tulee Applen oma höyste `git`-työkalusta, mutta suosittelen asentamaan Homebrew:n hallinnoiman version.

```bash
# Asenna
$ brew install git

# Tarkista että on asentunut
$ git --version
git version 2.42.0

# Varmista, että lokaationa on nimenomaan Homebrew:n asennuskansio
# EI SIIS /usr/bin/git vaan alla näkyvä tuloste
$ type git
git is /opt/homebrew/bin/git

# Mikäli yllä oleva tuloste viittaa /usr/bin-kansion executableen, aja seuraava
# komento ja kokeile uusiksi
$ rehash
```

## Valinnainen: Apple Keychain passphraseille

Passphrasen täyttäminen joka git- tai sshs-komennon yhteydessä on ärsyttävää. Tähän löytyy ratkaisuna ssh-agent. MacOS:ssä on mahdollista käyttää Applen omaa Keychainiä säilönä näille avaimille.

Nykyään vakio shelli macOS:ssä on Z Shell eli lyhyemmin `zsh` - tämä on siis Bashin korvaaja macOS:ssä. Helppo tapa ratkaista avaimien säilöminen Keychainiin on asentaa `Oh My Zsh`-niminen framework shell-konfiguraation hallintaan, ja pyytää sen pluginia hoitamaan koko homman.

Asenna [Oh My Zsh](https://ohmyz.sh/) sen oman sivuston ohjeiden mukaan. Sinun tarvitsee ajaa vain yksi komento.

Tämän jälkeen lisää seuraavat rivit `.zshrc`-tiedostoon:

```bash
# Choose Oh My Zsh plugins as whitespace list
# Example:
# plugins=(a-plugin another-plugin third-plugin)
plugins=(ssh-agent)

# Tell ssh-agent plugin to use Keychain.
zstyle :omz:plugins:ssh-agent ssh-add-args --apple-load-keychain

# Yllä olevien rivien pitäisi olla tiedostossa ENNEN seuravaanlaista riviä:
# source $ZSH/oh-my-zsh.sh
```

Tämän jälkeen voit lisätä avaimen passphrasen macOS:n keychainiin:
```bash
$ ssh-add --apple-use-keychain ~/.ssh/id_ed25519
  Enter passphrase for /Users/username/.ssh/id_ed25519: *******
  Identity added: /Users/username/.ssh/id_ed25519 (etunimisukunimi@kamk.fi macbook)
```

## Valinnainen: Git Credential Manager Core

Git Credential Manager Core on ohjelma, joka auttaa sinua kirjautumaan git-palveluihin. Se on erityisen hyödyllinen, jos haluat kirjautua esimerkiksi GitHubiin HTTPS:n avulla.

```bash
brew tap microsoft/git 
brew cask install git-credential-manager-core
```


## Valinnainen: Asenna Oh My Zsh

Mikäli haluat käyttää ssh-agenttia, helpoin tapa siihen Z Shellin kanssa on [Oh My Zsh](https://ohmyz.sh/), joka on Zsh:n konfiguraatioden hallintaa varten luotu framework.