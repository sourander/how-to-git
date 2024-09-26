!!! warning

    Huomaa, että tämä on edistyneille käyttäjille. Mikäli et ole varma, tarvitsetko tätä, et tarvitse tätä. Jos olet luonut ja testannut SSH-avainparin, jatka esimerkiksi [Soolokäyttäjän ohjeeseen](../../kaytto/soolokayttaja.md)

Ohjelman `ssh-agent` käyttö ei ole pakollista, mikäli luomasi avain on vakiokansiossa (`~/.ssh/`) ja vakionimellä (esim, `id_ed25519`), mutta agentin käyttö helpottaa siten, että sinun ei tarvitse syöttää passphrasea joka kerta kun haluat kirjautua palveluun. SSH-agentin avulla on siis mahdollista saavuttaa "best of both worlds", eli (1) passphrasella turvattu yksityinen avain, joka suojaa avainta mikäli se päätyy vääriin käsiin, ja (2) helppokäyttöinen ssh-avain, joka ei vaadi passphrasea jokaisen git fetch, git push ynnä muun operaation yhteydessä.

Mikäli `ssh-agent` on oikein konfiguroitu, sinun pitäisi voida kirjoittaa `ssh-add -l`, ja komennon pitäisi palauttaa sinun avaimesi tiedot. Lisäksi ympäristömuuttujat `SSH_AUTH_SOCK` sekä `SSH_AGENT_PID` sisältävät arvoja. Ne voit tulostaa komennolla: `printenv | grep SSH` tai yksitellen komennoilla `echo $SSH_AGENT_PID` sekä `echo $SSH_AUTH_SOCK`.

#### Windows-käyttäjälle

Valitettavasti `ssh-agent` ei käynnisty automaattisesti Git Bash:n yhteydessä. Tämä vaatii muutoksia shellin konfiguraatiotiedostoon. Ohjeet tähän löytyy [GitHubin dokumentaatiosta](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases?platform=windows#auto-launching-ssh-agent-on-git-for-windows).

#### macOS-käyttäjälle

Mikäli olet macOS-käyttäjä, sinulla ei ole Git Bashiä vaan todennäköisimmin Z Shell eli lyhyemmin `zsh`. Tällöin yksi tapa ratkaista ongelma on asentaa `Oh My Zsh`-niminen framework shell-konfiguraation hallintaan. Sen asentaa yhdellä komennolla, joka löytyy [Oh My Zsh -sivustolta](https://ohmyz.sh/).

Tämän jälkeen lisää seuraavat rivit `.zshrc`-tiedostoon:

```bash
# Choose Oh My Zsh plugins
plugins=(git ssh-agent)

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