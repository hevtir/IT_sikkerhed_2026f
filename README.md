# Opgave med test strategier
Opgaven er baseret på password validering.
Eksemplerne kan tages i brug, for at teste om logikken i koden virker (for at kvalitetssikre og for sikkerheds-mæssige grunde)

1. Ækvivalensklasser

Vi har følgende klasser:

* Gyldig klasse: et password der opfylder alle krav
* Ugyldige klasser:
    - Uden tal
    - Uden bogstaver
    - Minimum 8 tegn

2. Grænseværdi test

Eksempel:
* Minimum passwordlængde: 8 tegn
* Maximum passwordlængde: 20 tegn
    - 7 tegn -> afvist (lige under)
    - 8 tegn -> accepteret (lige på)
    - 9 tegn -> accepteret (lige over)
    - 20 tegn -> accepteret (maksimum grænse)
    - 21 tegn -> afvist (over grænseværdien)

Passwordet tjekkes, om det er under, lig eller over grænseværdien. 

3. CRUD(L) test
CRUD-testen bruges til at teste funktionaliteten i systemet.

* Create: Oprettes der et password?
* Read: Kan man se passwordet? (fra admins side)
* Update: Kan man redigere/opdatere passwordet?
* Delete: Kan passwordet slettes?
* (List): Kan man se en liste over alle passwords?

4. Cycle process test

* Bruger trykker "Glemt password"
* System sender reset-link
* Bruger vælger nyt password
* System opdaterer password
* Bruger kan logge ind igen

Dette testes som en proces i flere trin, hvor man tjekker at hele flowet virker.

5. Test pyramiden
Denne metode beskriver hvordan tests bør fordeles:

* Unit tests: Passwordvalidering og login-logik
* Integration tests: Login sammen med brugerdata
* System tests: Fuldt login-flow

6. Decision table test
Decision table testing bruges, når systemets adfærd afhænger af flere betingelser samtidig. Tabellen viser alle kombinationer af input og det forventede resultat.

| Bruger findes | Password korrekt | Konto låst | Resultat       |
| ------------- | ---------------- | ---------- | -------------- |
| Ja            | Ja               | Nej        | Login godkendt |
| Ja            | Nej              | Nej        | Login afvist   |
| Ja            | Ja               | Ja         | Konto låst     |
| Nej           | –                | –          | Login afvist   |

# Security Gates
Testene placeres i følgende security gates:

* Pre-commit: Unit tests
* CI pipeline: Unit og integration tests
* Før release: System tests

Dette sikrer, at sikkerhedsfejl opdages så tidligt som muligt.