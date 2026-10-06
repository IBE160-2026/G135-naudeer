# Tilbakemelding på product brief

| | |
|---|---|
| **Gruppe** | G135 – G135-naudeer |
| **Product brief** | `product-brief.md` (commit `c6c71e7`) |
| **Tilbakemelding fra** | Faglærer i IBE160 (utarbeidet med KI-støtte) |
| **Dato** | 2026-10-06 |

## Samlet vurdering

- **Godt utgangspunkt med justeringer.** Gruppen kan gå videre og innarbeide punktene under.

**Det som er bra:**

1. Én tydelig kjerneflyt: legge ut en gjenstand → be om lån for bestemte datoer → godta eller avslå → registrere henting og tilbakelevering. Dere sier selv at dere vil redusere oppdagelsesfunksjoner før dere kutter tilgangskontroll eller kjerneflyten.
2. Svært gode funksjonelle suksesskriterier: automatiske tester skal sjekke at overlappende godkjente lån avvises og at en bruker ikke kan endre andres annonser eller beslutninger. Det er konkrete regler som kan bli tester direkte.
3. Bemerkelsesverdig ærlig og gjennomtenkt. Problemet er formulert som en hypotese, eksempelet med klappbordet er merket som illustrasjon, og dere skiller tydelig mellom kursprosjektet og en eventuell virksomhet. Grensene (ingen betaling, depositum, forsikring, offentlige adresser eller live chat) er tydelige.

**De viktigste endringene:**

1. **Skill mellom det appen skal kunne og pilotmålene.** «Ten volunteer participants, fifteen listings and five completed real loans during a four-week pilot» og samtalene om lånebehov er gode, men avhenger av rekruttering og tid etter at prototypen er ferdig. Gjør det tydelig at de funksjonelle kriteriene er det som avgjør om v1 er ferdig, og at piloten er en bonus. Planlegg piloten tidlig nok, eller merk den som valgfri.
2. **En ekte pilot krever en publisert app.** Naboer i Trolla kan ikke teste en app som bare kjører lokalt. Publisering, personvern, samtykke og sletting er krevende. Vurder om brukertestene kan gjøres med appen kjørende på deres egen maskin, eller planlegg publisering som et eget, senere trinn.
3. **Rydd i v1-listen.** Scope inneholder også enkle profiler, søk og filtrering, avlysning og minimale rapporterings- og fjerningsverktøy for en pilotadministrator. Det gir tre roller (eier, låner, administrator). Marker hvilke deler som er «må ha» for kjerneflyten og hvilke som kan vente.

## Vanskelighetsgrad og gjennomførbarhet

### Vurdert vanskelighetsgrad

- **Middels**

**Sammenlignbart med:** 2) AI CV- og søknadsassistent (middels) i omfang og krav til personvern. TrollaDel har ikke KI i appen, men flere brukere som påvirker hverandre, en statusflyt med datoregler og tilgangskontroll per lån. Det er mer enn en enkel CRUD-app som 6) To-do-liste med smarte etiketter.

**Begrunnelse:**

| Faktor | Nivå (lav / middels / høy) | Kommentar |
|---|---|---|
| Domenelogikk – hvor mange og hvor kompliserte regler og beregninger må stemme? | middels | Statusflyt for lån (forespurt, godtatt, avslått, avlyst, hentet, levert, forfalt), overlappende datoer og regler for hvem som kan endre hva. |
| Datamodell – antall entiteter og relasjoner mellom dem | middels | Bruker, profil, gjenstand, bilde, låneforespørsel, statushendelse og rapport. |
| Brukere, roller og innlogging | middels | Eier, låner og pilotadministrator, med innlogging og deling av kontaktinfo først etter godkjenning. |
| KI-funksjonalitet i appen, f.eks. kall til språkmodell, prompts i koden og håndtering av usikre svar | lav | Ingen KI i appen. Det er greit, og det forenkler kjøring og testing. |
| Integrasjoner og eksterne tjenester, f.eks. API-er, betaling og e-post | lav | Ingen betaling eller eksterne tjenester. E-postvarsler er ikke nevnt. Bestem om varsler skal vises bare i appen. |
| Sanntid, samtidighet eller flere brukere som påvirker hverandre | middels | To lånere kan be om samme periode. Godkjenning må hindre overlapp også når to forespørsler behandles samtidig. |
| Filhåndtering, f.eks. opplasting, PDF-lesing og eksport | lav | Ett bilde per gjenstand. Begrens størrelse og filtype. |
| Sikkerhet og personvern | høy | Kontaktinfo, omtrentlig område og lånehistorikk for ekte naboer. Dere har allerede tenkt på samtykke, dataminimering og sletting, og det er bra. |

**Hva vanskelighetsgraden betyr for dere:**

- _Middels:_ Et godt balansert valg. Pass på at kjerneflyten blir ferdig og stabil før dere legger til mer. Dere har allerede formulert dette selv. Hold fast ved det når det blir travelt.

### Gjennomførbarhet med BMAD og Claude Code

Dere skal planlegge med BMAD (product brief → PRD → arkitektur → epics og stories) og implementere med Claude Code. Vurderingen under tar hensyn til at det må være tid til hele denne flyten, og til testing, retting og README til slutt.

| Spørsmål | Vurdering (OK / risiko / stor risiko) | Kommentar |
|---|---|---|
| **Tid og omfang** – kan v1 realistisk bli ferdig og stabil i løpet av semesteret, med tid til flere iterasjoner? | risiko | Kjerneflyten er realistisk for én person. Profiler, søk, administratorverktøy og en fire ukers pilot med publisering gjør det stramt. |
| **BMAD-flyten** – er briefen konkret nok til at PRD, arkitektur og stories kan lages uten store hull, og blir det overkommelig mange stories? | OK | Briefen er konkret nok til en god PRD, med tydelige regler og grenser. BMAD er ikke satt opp i repoet ennå. |
| **Egnet for Claude Code** – bruker løsningen en vanlig, godt dokumentert teknologistakk som Claude Code håndterer godt, eller krever den nisjeteknologi, spesialmaskinvare eller mye manuell konfigurasjon? | OK | En responsiv webapp med database og innlogging er godt egnet. |
| **Kontroll på KI-ens arbeid** – kan gruppen selv avgjøre om koden gjør det riktige? Krever domenet kunnskap gruppen ikke har, f.eks. avanserte beregninger eller fagregler, så er det vanskelig å kvalitetssikre. | OK | Reglene er enkle å forstå, og dere kan selv avgjøre om et lån håndteres riktig. |
| **Testbarhet** – finnes det tydelige regler og forventede resultater som tester kan skrives mot? | OK | Overlapp, tilgangskontroll og statusoverganger er allerede formulert som testkrav. |
| **Kjørbar for sensor** – kan appen kjøres lokalt etter README, uten gruppens nøkler, betalte kontoer eller egen infrastruktur? | OK | Uten KI og eksterne tjenester kan appen kjøres lokalt. Lag testbrukere (eier, låner, administrator) og eksempelgjenstander. |
| **Avhengigheter og kostnader** – krever løsningen betalte API-er, f.eks. språkmodeller, og finnes det en plan for kostnad, testmodus eller mock-data? | risiko | Appen trenger ingen betalte API-er. En ekte pilot krever likevel publisering, som kan koste penger og krever drift. |

**Konklusjon om gjennomførbarhet:**

- **Gjennomførbart med justert omfang.** Se forslagene under.

**Forslag til justering av omfang eller vanskelighetsgrad:**

1. **V1 (må ha):** innlogging, legge ut gjenstand med bilde, liste over gjenstander, låneforespørsel med datoer, godta/avslå med overlappsjekk, avlysning, henting og tilbakelevering, forfalte lån synlige, og kontaktinfo delt først etter godkjenning.
2. **Senere trinn:** søk og filtrering, administratorverktøy, profiler med historikk og publisering for en ekte pilot. Hvis dere ønsker en KI-funksjon, kan forslag til kategori og beskrivelse ut fra bildet av gjenstanden være en avgrenset utvidelse som løfter vanskelighetsgraden.

## Hvorfor product brief er viktig for mappen

Product brief er utgangspunktet for PRD, arkitektur, stories og til slutt koden. Del 1 av mappen vurderes blant annet på om sensor kan følge en sporbar vei fra plan til ferdig app. Den vurderes også på om appen gjør det dere har beskrevet, om den er testet, om den er godt designet, og om den kan kjøres etter README. Et uklart, for stort eller for lite brief gjør alt dette vanskeligere senere. Det er mye enklere å rette nå enn sent i semesteret.

## 1. Gjennomgang av briefens deler

| Del av brief | Status | Kommentar |
|---|---|---|
| Executive Summary – er det klart hva appen er, og hvilket problem den løser? | OK | Tydelig: en nettside for utlån i nabolaget med én komplett reise i første versjon. |
| The Problem – er problemet konkret, med reelle situasjoner og brukere? | Juster | Godt formulert som hypotese, men ennå ikke underbygd. Noen få korte samtaler med naboer før PRD ville styrket briefen. |
| The Solution – beskriver løsningen brukeropplevelsen, ikke bare teknologi? | OK | Hele flyten er beskrevet fra brukerens side, inkludert forfalte lån og skjult adresse. |
| What Makes This Different – er vurderingen ærlig og realistisk? | OK | Svært ærlig: ikke unik, ingen teknisk vollgrav, lokale kontakter er en mulighet, ikke en fordel. |
| Who This Serves – er primærbrukerne tydelige, og vet vi hva de trenger? | OK | Lånere og utlånere med konkrete behov, og administrator som tydelig støtterolle. |
| Success Criteria – kan kriteriene faktisk sjekkes eller testes? | Juster | Funksjonell kvalitet og brukbarhet er gode og testbare. Pilot- og forretningskriteriene avhenger av rekruttering og bør merkes som valgfrie. |
| Scope – er det klart hva som er med i første versjon, og hva som ikke er det? | Juster | Svært tydelig hva som er ute. V1-listen bør deles i «må ha» og «hvis tid». |
| Vision – henger visjonen sammen med resten uten å blåse opp omfanget? | OK | Trinnvis og nøktern, med tydelig skille mellom kursprosjekt og mulig virksomhet. |

## 2. Utgangspunkt for del 1 av mappen

Punktene følger kriteriene i sensorveiledningen for del 1. Vektene i parentes viser hvor mye hvert kriterium teller i del 1.

| Kriterium i del 1 | Hva briefen bør legge til rette for | Status | Kommentar |
|---|---|---|---|
| **1. Prosess og KI-styring** (30 %) | Brief som er presis nok til at PRD og stories kan bygges direkte på den, slik at krav kan spores fra brief til kode. | Juster | Briefen er presis nok. Sett opp BMAD i repoet og lag PRD, der hver regel får en ID som kan spores til tester. |
| **2. Funksjonalitet og omfang** (20 %) | Realistisk omfang for gruppen og semesteret: en tydelig kjerneflyt som kan bli ferdig og stabil, og nok innhold til å vise reell funksjonalitet. | OK | Tydelig kjerneflyt med nok innhold, og en god plan for hva som kuttes først. |
| **3. Kvalitetssikring og testing** (15 %) | Suksesskriterier og funksjoner som er konkrete nok til å bli testtilfeller. | OK | Overlapp og tilgangskontroll er allerede formulert som automatiske tester. Brukertesten med fem voksne er godt beskrevet. |
| **4. Design og brukeropplevelse** (10 %) | Tydelige brukere og brukssituasjoner som designet kan bygges rundt, gjerne med de viktigste skjermbildene eller flytene skissert. | Juster | Skisser gjenstandslisten, forespørselen med datovalg og «mine lån». Tydelige statuser og tomtilstander blir viktige. |
| **5. Kodekvalitet og arkitektur** (10 %) | Teknologivalg som er begrunnet og ikke mer komplekse enn appen trenger. | OK | Ingen teknologi er valgt ennå. Én webapp med én database holder. |
| **6. README og kjørbarhet** (10 %) | Løsning som andre kan kjøre lokalt uten betalte kontoer, og uten tilgang til gruppens egne tjenester og nøkler. | OK | Godt utgangspunkt uten eksterne tjenester. Planlegg testbrukere og eksempeldata i README. |
| **7. Ryddighet i repoet** (5 %) | En plan for hvor hemmeligheter, testdata og dokumentasjon skal ligge. | Juster | Hold eventuelle ekte pilotdata og samtykker helt utenfor det offentlige repoet. Bruk bare oppdiktede testdata i repoet. |

## 3. Neste steg for gruppen

1. Del v1 i «må ha» og «hvis tid» i briefen, og merk pilotmålene som valgfrie.
2. Bestem om piloten skal gjennomføres med publisert app eller som brukertester på egen maskin, og skriv valget inn i briefen.
3. Sett opp BMAD i repoet og lag PRD med statusflyten for lån beskrevet som regler med forventet resultat.

Oppdater product brief i repoet når dere har gjort endringene, slik at historikken viser hvordan planen utviklet seg. Det er en del av prosessen sensor ser etter.
