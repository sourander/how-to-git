Tyypillisesti Git-palveluihin (GitLab, Github, Bitbucket jne.) voi tunnistautua kolmella eri tavalla:

* Käyttäjätunnuksella ja salasanalla
    * Tätä käytetään useimmiten kun palveluun kirjaudutaan verkkoselaimella.
    * `git`-komentojen kanssa tämä ei ole suositeltua, ja osa palveluntarjoajista on estänyt jopa koko tavan.
* Token
    * Token ei pelkästään tunnistaudu vaan myös autorisoituu.
    * ... eli token sisältää sekä henkilöllisyyden että jonkin käyttöoikeuksien paletin, joka tunnetaan nimellä scope. 
    * `git`-komentojen kanssa tätä voi käyttää, ja onkin suositeltu tapa esimerkiksi automatisaatiossa. Mikäli token vuotaa, sillä voi tehdä vain scopen suhteen rajatut actionit, ja tokenin pääsy on helppo peruuttaa (eng. revoke).
* SSH-avainpari
    * SSH on suositeltu tunnistautumisen tapa peruskäytössä.
    * Toisin kuin yllä olevissa metodeissa, varsinaista salasanaa/tokenia ei koskaan lähetetä verkon yli palvelimelle. Tämän mahdollistaa asymmetrinen salaus.

Mikäli olet epävarma, käytä ssh:ta (tai https:ää). Mikäli olet edistyneempi käyttäjä, voit harkiten käyttää tokeneita sille sopivissa käyttötapauksissa.