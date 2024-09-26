# Usean SSH-avaimen käyttö (Advanced)

!!! warning

    Huomaa, että tämä on edistyneille käyttäjille. Mikäli et ole varma, tarvitsetko tätä, et tarvitse tätä. Jos olet luonut ja testannut SSH-avainparin, jatka esimerkiksi [Soolokäyttäjän ohjeeseen](../../kaytto/soolokayttaja.md)

Mikäli käytät useita eri avaimia, sinun pitää kertoa ssh-clientille, mitä avainta käytetään mihinkin palveluun. Tämä onnistuu ==manuaalisesti== ssh-komennon parametrilla:

```sh
$ ssh -i ~/.ssh/id_keyfile user@host
```

Mikäli haluat luoda eri avaimet eri palveluja varten ja käyttää niitä ==automaattisesti==, tarvitset konfiguraatiotiedoston `~/.ssh/config`, jonka sisältö on esimerkiksi. Tiedoston luominen on tarkkaa käsipeliä ja saattaa riippua esimerkiksi käytetystä käyttöjärjestelmästä hieman. Mikäli sinulla ei ole tarvetta tälle, älä tee sitä.

```sh title="~/.ssh/config"
Host github.com
  IdentityFile ~/.ssh/github
  IdentitiesOnly yes
Host example.com
  IdentityFile ~/.ssh/example
  IdentitiesOnly yes
Host short_alias
  HostName some.very.long.aws.instance.name.amazonaws.com/
  User ec2-user
  Port 22
  IdentityFile ~/.ssh/something
  IdentitiesOnly yes
```
