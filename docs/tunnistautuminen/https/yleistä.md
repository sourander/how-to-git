Tässä materiaalissa ohjeistetaan toistaiseksi vain SSH-tunnistautuminen. Tämä kansio on placeholder mahdollista tulevaisuuden käyttöä varten. Kun kloonaat repositoriota, varmistathan, että valitset `Clone`-nappulan alta SSH:n.

!!! warning

    Ethän käytä HTTPS:ää on-prem Gitlabin kanssa (eli repo.kamit.fi). Se ei tue Git Credential Manager Corea, joten joudut syöttämään käyttäjätunnuksen ja salasanan. Tämä on turvallisuusriski. Käytä SSH:tä.

Mikäli käytät HTTPS:ää esimerkiksi Gitlab ==Cloudin== tai Githubin kanssa, kannattaa varmistaa että sinulla on Git Credential Manager asennettuna. Tämän asennus riippuu käyttöjärjestelmästä. Lue lisää [Git Tools - Credential Storage](https://git-scm.com/book/en/v2/Git-Tools-Credential-Storage) tai [Git Credential Manager reposta](https://github.com/git-ecosystem/git-credential-manager).