# Besvarelse - Refleksjon og Analyse

**Student:** Rim

**Studentnummer:** rikas0685

**Dato:** 01.03.26

---

## Del 1: Datamodellering

### Oppgave 1.1: Entiteter og attributter

**Identifiserte entiteter:**

[Skriv ditt svar her - list opp alle entitetene du har identifisert]
Entitetene jeg har identifisert: 
Kunder
sykkelstasjoner
sykkel
system 



**Attributter for hver entitet:**

[Skriv ditt svar her - list opp attributtene for hver entitet]

Kunder: mobilNr, epost, fornavn, etternavn, betale, betalingskort 
sykkelstasjoner: sykkel, betaling, lås, sykkelstativ 
sykkel: utleietidspunkt, innleveringstidspunkt, ID, sykkelstasjon, lås, tidsrom
system: sykkelstasjoner, kunder, sykler, sykler tilgjengelige, stasjoner, utleide sykler, registrert betaling

### Oppgave 1.2: Datatyper og `CHECK`-constraints

**Valgte datatyper og begrunnelser:**

[Skriv ditt svar her - forklar hvilke datatyper du har valgt for hver attributt og hvorfor]

Kunder: 
mobilNr (Integer), Fordi det er hele nummer og tlf nummer kan ikke inneholde desimaler. 
epost(char), fornavn(char), fordi det er teskst. 
etternavn (char), fordi det er teskt. 
betaling (Decimal), fordi det er ikke sikkert på at tallet er heltal eller har desimaler. 
betalingskort (Integer), fordi betalingskort inneholder ikke desimaler. 

sykkelstasjoner: 
sykkelID (Integer), fordi det er ikke vanlig for en id å ha desimaler. 
betaling(Decimal), fordi det er ikke bestemt om beløpet har desimaler eller ikke. 
lås(boolean), for å se om låsen er tilgjengelig eller ikke, true or false. 
sykkelstativ(boolean), for å se hvilke sykkelstativer er tilgjengelige 
sykler tilgjengelige(boolean), for å se hvilke sykler som er tilgjengelige. 

sykkel: 
utleietidspunkt (TimeStamp), fordi utleing av sykler blir beregnet med tideb den er lånt til tiden den er returnert.
innleveringstidspunkt(TimeStamp), fordi utleing av sykler blir beregnet med tideb den er lånt til tiden den er returnert.
sykkelID(Integer), fordi det er ikke vanlig for en id å ha desimaler. 
sykkelstasjon(char), for å vite hvilke sykkelstasjon det gjelder med navn eller sted. 
lås(Integer), 
betaling(Decimal)

system: 
sykkelstasjoner(char), for å ha en oversikt over sykkelstasjoner
kunder(char), for å holde oversikt over hvilke kunder som har benyttet servicen 
sykkelID (Integer), fordi det er ikke vanlig for en id å ha desimaler. 
sykler tilgjengelige(Boolean), holder oversikt over om sykler er tilgjengelige i sykkelstasjonene og om de er returnert. 
utleide sykler (integer), for å holde oversikt over hvor mange sykler som er leid. 
registrert betaling(Boolean), fordi true eller false om en betaling er gjort 

**`CHECK`-constraints:**

[Skriv ditt svar her - list opp alle CHECK-constraints du har lagt til og forklar hvorfor de er nødvendige]

CHECK (pris >= 0)
CHECK (beløp >= 0)
CHECK (antall_stativ > 0)
CHECK (status IN ('tilgjengelig','utleid'))
CHECK (betalingsstatus IN ('betalt','ikkeBetalt'))
CHECK (innleveringstidspunkt IS NULL OR innleveringstidspunkt > utleietidspunkt)

sikrer:
ingen negative priser
gyldige staus av tilgjengelige sykler 
riktig tidsrekkefølge 

**ER-diagram:**

[Legg inn mermaid-kode eller eventuelt en bildefil fra `mermaid.live` her]



erDiagram
  Kunder ||--o{ sykkelstasjoner : places
  sykkelstasjoner ||--o{ sykkel : contains
  system ||--|{ sykkelstasjoner : manages
  
  Kunder {
    int KundeID
    int mobilNr
    char epost
    char fornavn
    char Etternavn
    double betale
    string betalingskort
  }

  sykkelstasjoner {
    int sykkelstasjonID (PK)
    int sykkelID
    decimal betaling
    boolean lås
    boolean sykkelstativ
    boolean syklerTilgjengelige
  }
  sykkel {
    timestamp utleietidspunkt
    timestamp innleveringstidspunkt
    int sykkelID
    char sykkelstasjon
    int lås
    decimal betaling
  }
  system {
    int systemID 
    int sykkelstasjonID
    int kundeID
    int sykkelID
    boolean syklerTilgjengelige
    int utleideSykler
    boolean registrertBetaling
  }
---

### Oppgave 1.3: Primærnøkler

**Valgte primærnøkler og begrunnelser:**

[Skriv ditt svar her - forklar hvilke primærnøkler du har valgt for hver entitet og hvorfor]

Kunder {
    int KundeID (PK)
    int mobilNr 
    char epost
    char fornavn
    char Etternavn
    double betale
    string betalingskort 
  }
Fordi KundeId er unikt for hver kunde og ingen andre kan ha det. 

  sykkelstasjoner {
    int sykkelstasjonID (PK)
    int sykkelID 
    decimal betaling
    boolean lås
    boolean sykkelstativ
    boolean syklerTilgjengelige
  }
Fordi hver sykkelID er unik for hver sykkel og ingen andre sykler kan ha samme id. 

  sykkel {
    timestamp utleietidspunkt
    timestamp innleveringstidspunkt
    int sykkelID (PK)
    char sykkelstasjon
    int lås
    decimal betaling
  }
  Fordi hver sykkelID er unik for hver sykkel og ingen andre sykler kan ha samme id. 

  system {
    int systemID (PK)
    int sykkelstasjonID (PK)
    int kundeID
    int sykkelID
    boolean syklerTilgjengelige
    int utleideSykler
    boolean registrertBetaling
  }
Fordi hver systemID er unik for hvert system og ingen andre system kan ha samme id. 

**Naturlige vs. surrogatnøkler:**

[Skriv ditt svar her - diskuter om du har brukt naturlige eller surrogatnøkler og hvorfor]

jeg har brukt surrogatnøkler fordi det er en stabil identifikasjon for hvert entitet og kan ikke endres eller gjenbrukes av andre som gjør dem unike. 


**Oppdatert ER-diagram:**

[Legg inn mermaid-kode eller eventuelt en bildefil fra `mermaid.live` her]

erDiagram
  Kunder ||--o{ sykkelstasjoner : manages
  Kunder ||--o{ system : interacts_with
  sykkelstasjoner ||--o{ sykkel : has
  system }o--|| sykkel : rents
  system ||--o{ Kunder : includes

  Kunder {
    int KundeID PK
    int mobilNr
    char epost
    char fornavn
    char Etternavn
    double betale
    string betalingskort
  }


  sykkelstasjoner {
    int sykkelstasjonID PK
    int sykkelID
    decimal betaling
    boolean lås
    boolean sykkelstativ
    boolean syklerTilgjengelige
  }


  sykkel {
    timestamp utleietidspunkt
    timestamp innleveringstidspunkt
    int sykkelID PK
    char sykkelstasjon
    int lås
    decimal betaling
  }
  

  system {
    int systemID PK
    int sykkelstasjonID
    int kundeID
    int sykkelID
    boolean syklerTilgjengelige
    int utleideSykler
    boolean registrertBetaling
  }

### Oppgave 1.4: Forhold og fremmednøkler

**Identifiserte forhold og kardinalitet:**

[Skriv ditt svar her - list opp alle forholdene mellom entitetene og angi kardinalitet]



**Fremmednøkler:**

[Skriv ditt svar her - list opp alle fremmednøklene og forklar hvordan de implementerer forholdene]

 Kunder {
    int KundeID PK
    int mobilNr
    char epost
    char fornavn
    char Etternavn
    double betale
    string betalingskort
  }


  sykkelstasjoner {
    int sykkelstasjonID PK
    int sykkelID
    decimal betaling
    boolean lås
    boolean sykkelstativ
    boolean syklerTilgjengelige
  }


  sykkel {
    timestamp utleietidspunkt
    timestamp innleveringstidspunkt
    int sykkelID PK
    char sykkelstasjon
    int lås
    decimal betaling
  }
  

  system {
    int systemID PK
    int sykkelstasjonID
    int kundeID
    int sykkelID
    boolean syklerTilgjengelige
    int utleideSykler
    boolean registrertBetaling
  }

**Oppdatert ER-diagram:**

[Legg inn mermaid-kode eller eventuelt en bildefil fra `mermaid.live` her]

---

### Oppgave 1.5: Normalisering

**Vurdering av 1. normalform (1NF):**

[Skriv ditt svar her - forklar om datamodellen din tilfredsstiller 1NF og hvorfor]

**Vurdering av 2. normalform (2NF):**

[Skriv ditt svar her - forklar om datamodellen din tilfredsstiller 2NF og hvorfor]

**Vurdering av 3. normalform (3NF):**

[Skriv ditt svar her - forklar om datamodellen din tilfredsstiller 3NF og hvorfor]

**Eventuelle justeringer:**

[Skriv ditt svar her - hvis modellen ikke var på 3NF, forklar hvilke justeringer du har gjort]

---

## Del 2: Database-implementering

### Oppgave 2.1: SQL-skript for database-initialisering

**Plassering av SQL-skript:**

[Bekreft at du har lagt SQL-skriptet i `init-scripts/01-init-database.sql`]

**Antall testdata:**

- Kunder: [antall]
- Sykler: [antall]
- Sykkelstasjoner: [antall]
- Låser: [antall]
- Utleier: [antall]

---

### Oppgave 2.2: Kjøre initialiseringsskriptet

**Dokumentasjon av vellykket kjøring:**

[Skriv ditt svar her - f.eks. skjermbilder eller output fra terminalen som viser at databasen ble opprettet uten feil]

**Spørring mot systemkatalogen:**

```sql
SELECT table_name 
FROM information_schema.tables 
WHERE table_schema = 'public' 
  AND table_type = 'BASE TABLE'
ORDER BY table_name;
```

**Resultat:**

```
[Skriv resultatet av spørringen her - list opp alle tabellene som ble opprettet]
```

---

## Del 3: Tilgangskontroll

### Oppgave 3.1: Roller og brukere

**SQL for å opprette rolle:**

```sql
[Skriv din SQL-kode for å opprette rollen 'kunde' her]
```

**SQL for å opprette bruker:**

```sql
[Skriv din SQL-kode for å opprette brukeren 'kunde_1' her]
```

**SQL for å tildele rettigheter:**

```sql
[Skriv din SQL-kode for å tildele rettigheter til rollen her]
```

---

### Oppgave 3.2: Begrenset visning for kunder

**SQL for VIEW:**

```sql
[Skriv din SQL-kode for VIEW her]
```

**Ulempe med VIEW vs. POLICIES:**

[Skriv ditt svar her - diskuter minst én ulempe med å bruke VIEW for autorisasjon sammenlignet med POLICIES]

---

## Del 4: Analyse og Refleksjon

### Oppgave 4.1: Lagringskapasitet

**Gitte tall for utleierate:**

- Høysesong (mai-september): 20000 utleier/måned
- Mellomsesong (mars, april, oktober, november): 5000 utleier/måned
- Lavsesong (desember-februar): 500 utleier/måned

**Totalt antall utleier per år:**

[Skriv din utregning her]

**Estimat for lagringskapasitet:**

[Skriv din utregning her - vis hvordan du har beregnet lagringskapasiteten for hver tabell]

**Totalt for første år:**

[Skriv ditt estimat her]

---

### Oppgave 4.2: Flat fil vs. relasjonsdatabase

**Analyse av CSV-filen (`data/utleier.csv`):**

**Problem 1: Redundans**

[Skriv ditt svar her - gi konkrete eksempler fra CSV-filen som viser redundans]

**Problem 2: Inkonsistens**

[Skriv ditt svar her - forklar hvordan redundans kan føre til inkonsistens med eksempler]

**Problem 3: Oppdateringsanomalier**

[Skriv ditt svar her - diskuter slette-, innsettings- og oppdateringsanomalier]

**Fordeler med en indeks:**

[Skriv ditt svar her - forklar hvorfor en indeks ville gjort spørringen mer effektiv]

**Case 1: Indeks passer i RAM**

[Skriv ditt svar her - forklar hvordan indeksen fungerer når den passer i minnet]

**Case 2: Indeks passer ikke i RAM**

[Skriv ditt svar her - forklar hvordan flettesortering kan brukes]

**Datastrukturer i DBMS:**

[Skriv ditt svar her - diskuter B+-tre og hash-indekser]

---

### Oppgave 4.3: Datastrukturer for logging

**Foreslått datastruktur:**

[Skriv ditt svar her - f.eks. heap-fil, LSM-tree, eller annen egnet datastruktur]

**Begrunnelse:**

**Skrive-operasjoner:**

[Skriv ditt svar her - forklar hvorfor datastrukturen er egnet for mange skrive-operasjoner]

**Lese-operasjoner:**

[Skriv ditt svar her - forklar hvordan datastrukturen håndterer sjeldne lese-operasjoner]

---

### Oppgave 4.4: Validering i flerlags-systemer

**Hvor bør validering gjøres:**

[Skriv ditt svar her - argumenter for validering i ett eller flere lag]

**Validering i nettleseren:**

[Skriv ditt svar her - diskuter fordeler og ulemper]

**Validering i applikasjonslaget:**

[Skriv ditt svar her - diskuter fordeler og ulemper]

**Validering i databasen:**

[Skriv ditt svar her - diskuter fordeler og ulemper]

**Konklusjon:**

[Skriv ditt svar her - oppsummer hvor validering bør gjøres og hvorfor]

---

### Oppgave 4.5: Refleksjon over læringsutbytte

**Hva har du lært så langt i emnet:**

[Skriv din refleksjon her - diskuter sentrale konsepter du har lært]

**Hvordan har denne oppgaven bidratt til å oppnå læringsmålene:**

[Skriv din refleksjon her - koble oppgaven til læringsmålene i emnet]

Se oversikt over læringsmålene i en PDF-fil i Canvas https://oslomet.instructure.com/courses/33293/files/folder/Plan%20v%C3%A5ren%202026?preview=4370886

**Hva var mest utfordrende:**

[Skriv din refleksjon her - diskuter hvilke deler av oppgaven som var mest krevende]

**Hva har du lært om databasedesign:**

[Skriv din refleksjon her - reflekter over prosessen med å designe en database fra bunnen av]

---

## Del 5: SQL-spørringer og Automatisk Testing

**Plassering av SQL-spørringer:**

[Bekreft at du har lagt SQL-spørringene i `test-scripts/queries.sql`]


**Eventuelle feil og rettelser:**

[Skriv ditt svar her - hvis noen tester feilet, forklar hva som var feil og hvordan du rettet det]

---

## Del 6: Bonusoppgaver (Valgfri)

### Oppgave 6.1: Trigger for lagerbeholdning

**SQL for trigger:**

```sql
[Skriv din SQL-kode for trigger her, hvis du har løst denne oppgaven]
```

**Forklaring:**

[Skriv ditt svar her - forklar hvordan triggeren fungerer]

**Testing:**

[Skriv ditt svar her - vis hvordan du har testet at triggeren fungerer som forventet]

---

### Oppgave 6.2: Presentasjon

**Lenke til presentasjon:**

[Legg inn lenke til video eller presentasjonsfiler her, hvis du har løst denne oppgaven]

**Hovedpunkter i presentasjonen:**

[Skriv ditt svar her - oppsummer de viktigste punktene du dekket i presentasjonen]

---

**Slutt på besvarelse**
