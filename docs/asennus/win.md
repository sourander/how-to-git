Asenna Git client: [Git for Windows](https://gitforwindows.org/). Ethän klikkaa autopilotilla `Next`-nappulaa, vaan toimit tunnollisen it-alan ammattilaisen tavoin ja luet kaikki vaihtoehdot läpi. Kiinnitä huomiota erityisesti seuraavissa kuvissa näkyviin vaihtoehtoihin. Asetukset säätävät järjestelmätason defaultteja ja tulevat kaikkiin konfiguraatiohin jatkossa defaulttina.

![Git Installer Default Editor Choice](../images/git-for-windows-installer-nano.png)

**Kuvio 1:** *Asennus pyytä sinua valitsemaan default editorin muun muassa commit messagejen kirjoittamista varten. Vakiona tarjottu vim ei ole aloittelijoita varten. On suositeltavaa valita Nano tai esimerkiksi Notepad++ (jos on asennettuna). Nano:lla pääsee pitkälle.*

![Git Installer Default Branch Name](../images/git-for-windows-installer-branch.png)

**Kuvio 2:** *Oletusbranchin nimi kannattaa vaihtaa vastaamaan nykypäivän standardia eli `main`. Juuri kukaan ei enää käytä sanaa master.*

![](../images/git-for-windows-pull-ff-only.png)

**Kuvio 3:** *On suositeltavaa, että et anna Gitin luoda mergejä sinun pyytämättäsi, ellei nimenomaan fast-forward onnistu.*

## Asennuksen jälkeen

1. Käynnistä asentamisen jälkeen tietokone uusiksi.
2. Käynnistä Start-menusta Git Bash.
3. Testaa `git --version`
4. Kun ohjelmisto on asennettu, siirry lukuun [Konfiguraatio](konfiguraatio.md).

Mikäli luit asennuksen tarjoamat vaihtoehdot huolella, ja asetit sinulle sopivat (tai suositellut) asetukset, säästyt varsinaisessa konfiguraatioiden laittamisessa yllättävän helpolla.