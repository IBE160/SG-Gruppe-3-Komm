# Refleksjonsrapport - Programmering med KI

## 1. Gruppeinformasjon

**Gruppenavn:** [SG-GRUPPE-3-KOMM]

**Gruppemedlemmer:**
- [Bjørnar Jensen 1] - [241595-ID/Bjornar.jensen@himolde.no]
- [Sten Otto Eilertsen 2] - [160808-ID/E-post]
- [Tobias André Torbergsen 3] - [241813/E-post]

**Dato:** [DD.MM.ÅÅÅÅ]

---

### 2.1 Oversikt over prosjektet
Målet med prosjektet er å utvikle en nettbasert applikasjon som genererer en personlig og adaptiv studieplan basert på brukerens eksamensdatoer, pensum, tilgjengelig studietid og progresjon. Systemet fordeler emner, planlegger repetisjon og justerer planen dynamisk når brukeren ligger foran eller bak. Målgruppen er universitets- og høyskolestudenter som forbereder seg til flere eksamener. Applikasjonen skal redusere stress og kognitiv belastning ved å automatisere planleggingen og støtte kontinuerlig fremgang gjennom datadrevet personalisering.

### 2.2 Arbeidsmetodikk
- **Fordeling av oppgaver:** Vi arbeidet i ukentlige workshops, roterte på skjermdeling og sørget for at alle fulgte utviklingen. Alle satte opp VS Code, GitHub og nødvendige verktøy lokalt for å muliggjøre individuelt arbeid.  
- **Samarbeidsverktøy:** Vi brukte GitHub for versjonshåndtering og branching, samt Teams for gruppesamarbeid.  
- **Bruk av KI-verktøy:** Vi brukte Gemini integrert i VS Code, vurderte fortløpende kvaliteten på LLM-forslagene og forbedret promptene våre gjennom iterative loops.


### 2.3 Teknologi og verktøy
[Liste over de viktigste teknologiene og verktøyene dere brukte]
- Frontend: [TypeScript,Tailwind, NextJS, HTML/CSS, Vercel]
- Backend: [Python/FastAPI]
- Database: [Supabase]
- KI-verktøy: [Gemini-flash, Gemini-pro, ChatGPT,Stich]
- Andre verktøy: [VS Code, BMAD-metodikk]


### 2.4 Utviklingsfaser
**Fase 0: Planlegging**  
Fase 0 bestod av å etablere et solid fundament for prosjektet gjennom strukturerte KI-drevne arbeidsprosesser. Vi startet med *workflow-init*, der KI genererte første versjon av `bmm-workflow-status.yaml`, som ga en tydelig oversikt over nødvendige aktiviteter, dokumenter og faser i BMAD-løpet.

Deretter gjennomførte vi flere *brainstorming sessions* med `/run-agent-task analyst *brainstorm`, som produserte egne markdown-dokumenter med innsikt og forslag. KI bidro til å strukturere ideer, identifisere problemområder og foreslå funksjonalitet vi ellers kunne oversett.

Vi utførte også en målrettet *research session* med `/run-agent-task analyst *research` for å vurdere tekniske alternativer for hvordan LLM-interactions burde orchestreres, noe som styrket beslutningsgrunnlaget for arkitektur og teknologi.

Til slutt konsoliderte vi arbeidet i et *product brief* via `/run-agent-task analyst *product-brief`, der KI analyserte brainstorming-materialet, research-funn og vårt proposal-utkast. Resultatet, `product-brief.md`, beskrev prosjektets mål, brukerbehov, funksjonelle krav og videre retning, og fungerte som et sentralt referansedokument for resten av BMAD-prosessen.


**Fase 1: Requirements and UX Design**  
I fase 1 gikk vi fra idé- og informasjonsinnsamling til å konkretisere prosjektets krav og brukeropplevelse. Vi startet med en *Planning*-fase der KI genererte et fullstendig Product Requirements Document (PRD) via `/run-agent-task pm *prd`. Dokumentet (PRD.md) beskrev funksjonelle krav, målgrupper, brukerbehov og tekniske rammer som skulle styre videre utvikling.

Deretter gjennomførte vi `/run-agent-task pm *validate-prd`, som resulterte i en *validation report*. Denne prosessen sikret at PRD-en var konsistent, gjennomførbar og i tråd med prosjektets mål. KI identifiserte uklarheter, svakheter og manglende sammenhenger, noe som styrket dokumentets kvalitet.

Den neste delen av fasen fokuserte på det visuelle og konseptuelle brukergrensesnittet. Gjennom `/run-agent-task ux-designer *create-ux-design` genererte KI omfattende UX-materiale, inkludert:
- `ux-design-specification.md`
- `ux-color-themes.html`
- `ux-design-directions.html`

Dokumentene inneholdt layout-forslag, navigasjonsstrukturer, designretninger og fargepaletter som dannet grunnlaget for senere frontend-utvikling. KI bidro til å tydeliggjøre hvordan produktet kunne se ut i praksis og hvilke brukeropplevelser som burde støttes.

Fasen avsluttet med en designvalidering via `/run-agent-task ux-designer *validate-ux-design`, der KI vurderte konsistens, brukervennlighet og samsvar mellom UX-materialet og PRD-kravene. Samlet ga fase 1 et klart og verifisert grunnlag for videre arbeid med teknisk arkitektur og implementering.

**Fase 2: Solutioning and Architecture**  
Fase 2 handler om å definere hvordan løsningen skal bygges og omforme krav, innsikt og design til en konkret, gjennomførbar systemarkitektur. Dette innebærer å etablere tekniske strukturer, avklare avhengigheter og beskrive hvordan systemets komponenter skal fungere sammen.

Et hovedsteg er *Solutioning*, der KI eller arkitektverktøy genererer et foreslått arkitekturdokument via `/run-agent-task architect *create-architecture`. Dokumentet beskriver systemkomponenter, datamodeller, API-strukturer, informasjonsflyt og teknologistack, og gir et helhetlig bilde av implementeringen.

Samtidig brytes kravene ned i epics og user stories gjennom `/run-agent-task pm *create-epics-and-stories`, som omformer funksjonelle behov til konkrete utviklingsoppgaver og tydeliggjør rekkefølgen i arbeidet.

Fasen inkluderer også *test-design* via `/run-agent-task tea *test-design`, hvor teststrategi og scenarier utformes. Dette gir et rammeverk for kvalitetssikring før kode skrives.

Til slutt gjennomføres en *Solutioning Gate Check* via `/run-agent-task architect *solutioning-gate-check`, som vurderer om arkitektur, epics og testgrunnlag er tydelige, konsistente og tilstrekkelige for videre utvikling. Gate-checken fungerer som en siste verifisering av at prosjektet har et solid fundament før implementasjonen starter.

Fase 2 fungerer som en bro mellom konsept og implementering og etablerer de strukturelle og organisatoriske rammene som muliggjør en systematisk og skalerbar utviklingsprosess.


**Fase 3: Implementation**  
Fase 3 handler om å omsette arkitektur og krav til funksjonalitet gjennom et sprint-basert utviklingsløp. Prosessen starter med `/run-agent-task sm *sprint-planning`, hvor KI genererer en sprintplan (`sprint-status.yaml`) som angir hvilke epics og stories som skal utvikles.

For hver epic opprettes en teknisk spesifikasjon via `/run-agent-task sm create-epic-tech-context`, etterfulgt av validering. Dette etablerer et tydelig teknisk grunnlag. Epicene brytes deretter ned i user stories, som følger en strukturert prosess: story creation, validation, context creation, ready-for-dev–markering og deretter utvikling.

Under implementasjonen gjennomgår hver story flere utviklings- og review-sykluser via `/run-agent-task dev *develop-story` og `/run-agent-task dev *code-review` før den godkjennes. Etterpå testes den gjennom `/run-agent-task sm *test-review`.

Når alle stories i en epic er ferdigstilt, avsluttes arbeidet med en `/run-agent-task sm *epic-retrospective`.  
Fase 3 fokuserer dermed på praktisk utvikling, kvalitetssikring og iterativ fremdrift innenfor en tydelig definert sprintworkflow.

---

### 3.1 Tekniske utfordringer

**Utfordring 1: KI-modellen forstod ikke BMAD-rammeverket**  
**Problem:**  
En av de største tekniske utfordringene var at Gemini ofte misforstod BMAD-metodikken, selv med klare instruksjoner. Modellen blandet faser og roller, hoppet over deler av prosessen eller ble for kreativ i stedet for å følge den etablerte strukturen. Dette førte til at vi ofte måtte restarte samtalen eller omskrive promptene flere ganger.

**Løsning:**  
Vi utviklet mer presise og strengt formulerte prompts der rolle, oppgave, metode, forventet output og begrensninger ble eksplisitt definert. Etter hvert fant vi en effektiv oppskrift: tydelige rammer, steg-for-steg-prompting og eksempler som viste hva modellen skulle hente fra BMAD. Dette tok tid, men ga mer stabile og relevante svar.

**KI sin rolle:**  
KI var både en støtte og en hindring. Når promptene fungerte, leverte modellen strukturerte bidrag som passet inn i BMAD-prosessen. Samtidig skapte svak kontekstforståelse, ustabil rollekontroll og varierende kvalitet ekstra arbeid, spesielt i prosjektets tidlige fase.


**Utfordring 2: Endringer i BMAD-rammeverket underveis i semesteret**  
**Problem:**  
BMAD-rammeverket ble oppdatert flere ganger i løpet av semesteret, noe som skapte utfordringer fordi dokumentasjon, eksempler og modellens tidligere kontekst ikke lenger samsvarte med den nye versjonen. Dette gjorde at vi måtte omformulere arbeid, endre promptstrukturer og lære KI den oppdaterte tolkningen av rammene.

**Løsning:**  
Vi håndterte dette ved å være fleksible og kontinuerlig justere prosessen etter endringene. Faglærer ga oppdaterte forklaringer, nye eksempler og tydelige rettelser, noe som gjorde tilpasningen enklere. Vi oppdaterte også prompts og arbeidsdokumenter slik at KI fikk klare instrukser basert på den nyeste BMAD-versjonen.

**KI sin rolle:**  
KI hjalp oss med å raskt omskrive dokumentasjon og tilpasse strukturen til de nye rammene, men ble samtidig forvirret av endringene og måtte læres opp på nytt. Dette ga ekstra arbeid, men også nyttig erfaring med prompt engineering og håndtering av kontekstversjoner.


### 3.2 Samarbeidsutfordringer

En sentral utfordring var å finne tidspunkt som passet for alle, siden vi var geografisk spredt og hadde ulike timeplaner. For å håndtere dette brukte vi direkte kommunikasjon via Teams og Messenger, noe som gjorde det mulig å avklare spørsmål raskt og opprettholde en effektiv dialog mellom møtene. Løsningen fungerte godt, men forutsatte fleksibilitet og aktiv deltakelse fra alle for å sikre god fremdrift.

### 3.3 KI-spesifikke utfordringer

Vi opplevde flere utfordringer direkte knyttet til bruken av KI-modeller i BMAD-prosessen.

**Utfordring 1: KI mistet kontekst i lange samtaler**  
Modellen hadde begrensninger i lange og komplekse dialoger. Selv med tydelig definerte roller og struktur kunne KI miste tråden, endre skrivestil eller ignorere BMAD-regler. Dette gjorde at vi ofte måtte starte nye økter, gjenta instruksjoner og minne modellen på rammeverket.

**Utfordring 2: KI ga selvsikre, men feilaktige svar**  
KI leverte tidvis overbevisende, men feilaktige svar innen både tekniske forklaringer, BMAD-artefakter og kode. Vi måtte derfor alltid verifisere utdata før videre bruk, noe som skapte ekstra arbeid når vi i utgangspunktet forventet at svaret var korrekt.

**Utfordring 3: Vansker med å generere riktige BMAD-menyer og struktur**  
Det var utfordrende å få KI til å produsere korrekte menyer og strukturelle elementer som BMAD krever. Selv ved tydelige instruksjoner leverte modellen ofte feil struktur, manglende punkter eller avvikende stil.

Ved hjelp av mer indirekte og styrende prompts klarte vi etter hvert å “lede” KI mot riktig BMAD-struktur. Dette krevde presise instrukser og flere iterasjoner, men ga gradvis mer treffsikre resultater.

---

### 4.1 Fordeler med KI-assistanse

**Effektivitet og produktivitet:**  
Bruken av KI gjorde at vi kunne jobbe betydelig raskere enn manuelt. KI guidet oss gjennom BMAD-maler og prosesser, noe som forenklet forståelsen av strukturen og hva som skulle produseres i hver fase. Den genererte også kodeutkast, som for eksempel Stich-mockups av dashboardet, forklarte funksjoner og foreslo forbedringer, noe som effektiviserte utviklingsarbeidet. Oppgaver som normalt ville krevd omfattende research ble løst på minutter.

**Læring og forståelse:**  
KI ga økt faglig innsikt ved å tilby forklaringer og eksempler når vi sto fast i tekniske eller metodiske spørsmål. Den fungerte til dels som en ekstra veileder ved å gi raske avklaringer og alternative perspektiver.


**Kvalitet på koden:**
- [Hvordan påvirket KI kodekvaliteten?]
- [Eksempler på forbedringer KI foreslo]

### 4.2 Begrensninger og ulemper

**Kvalitet og pålitelighet:**  
Selv om KI var et nyttig verktøy, var kvaliteten på svarene svært varierende. Modellen kunne gi selvsikre, men feilaktige eller mangelfulle forklaringer, misforstå oppgaven, forenkle for mye eller fokusere på irrelevante detaljer. Dette gjorde at vi måtte dobbeltsjekke og justere store deler av dokumentasjonen og koden som ble generert.

Vi opplevde også at KI tidvis “gjorde seg vrang”, særlig når den tolket prompten feil. Den kunne gi irrelevante svar, ignorere instruksjoner eller foreslå løsninger uten sammenheng med prosjektet. I tillegg hallusinerte den av og til konsepter eller teknologier som ikke var relevante.

Når konteksten ble forvirret, var det ofte nødvendig å starte nye samtaler for å unngå ytterligere misforståelser. Selv om kvaliteten økte med svært presise og detaljerte prompts, krevde dette ekstra arbeid, og vi kunne aldri bruke KI-utdata direkte uten manuell kvalitetssikring.

**Avhengighet og forståelse:**  
KI gjorde mange oppgaver enklere, og vi merket at det tidvis ble lett å bli for avhengige av verktøyet. Siden KI alltid var tilgjengelig med raske svar, kunne det friste å spørre modellen før vi forsøkte å løse utfordringene selv, noe som reduserte den naturlige refleksjonen i arbeidsprosessen.

Modellen ga ofte gode og overbevisende forklaringer, noe som kunne skape en falsk følelse av forståelse. Det var enkelt å akseptere et svar som “godt nok” uten å gå gjennom resonnementet bak. Samtidig bidro den manuelle kvalitetssikringen vi måtte gjøre til økt læring: gjennom å analysere, rette og forbedre KI-utdata utviklet vi både metodisk forståelse og teknisk innsikt, noe som dempet risikoen for overavhengighet.

**Kreativitet og problemløsning:**  
KI påvirket kreativiteten vår ved at den ofte satte retningen før vi utforsket egne ideer. Når KI foreslo løsninger eller strukturer, ble disse lett stående som utgangspunkt, noe som kunne gjøre vår kreative prosess mer reaktiv enn initiativdrevet.

Modellen kunne også skape et “tunnelsyn”, der forslagene ledet oss inn i én bestemt løsningsretning selv om andre muligheter kunne vært mer interessante. Selv om KI effektiviserte arbeidet, opplevde vi at den til tider begrenset den frie, utforskende problemløsningen som oppstår uten forhåndsbestemte forslag.

### 4.3 Sammenligning: Med og uten KI

Arbeidet med prosjektet ville vært betydelig annerledes uten KI. Mange oppgaver i BMAD-prosessen—som å utforme dokumenter, foreslå strukturer og utvikle brukerhistorier—ville tatt langt lengre tid. KI fungerte som en rask sparringspartner som genererte førsteutkast og hjalp oss videre når vi sto fast. Uten denne støtten ville vi måtte løse alt manuelt, med mer research, flere diskusjoner og en langt tregere iterasjonstakt.

De mest krevende delene uten KI ville vært å etablere en tydelig struktur i BMAD-fasene og å produsere konsistente tekniske beskrivelser og krav. Samtidig ville enkelte aspekter vært enklere, siden vi da unngikk KI-relaterte utfordringer som feil svar, tapt kontekst og misforståelser. Arbeidsflyten ville blitt mer forutsigbar, men vesentlig saktere.

Vi vurderer at sluttresultatet trolig ville vært svakere uten KI. Verktøyet gjorde det mulig å jobbe mer effektivt og produsere mer omfattende dokumenter innenfor tidsrammen. Uten KI ville vi lært mer på egen hånd, men på bekostning av fremdrift og kvalitet. Kombinasjonen av KI-støtte og menneskelig vurdering ga etter vår vurdering et bedre sluttprodukt enn noen av delene alene.

### 4.4 Samlet vurdering

Totalt sett vurderer vi at KI hadde en klart positiv innvirkning på prosjektet. Til tross for utfordringer knyttet til kvalitet, kontekst og konsistens, gjorde KI det mulig å jobbe raskere, holde struktur i BMAD-prosessen og produsere mer omfattende dokumenter enn vi ville klart alene. KI støttet både planlegging, dokumentasjon og utvikling, og gjorde iterasjon og forbedring enklere.

Samtidig var det viktig å ikke stole blindt på verktøyet. Den sentrale lærdommen var at KI fungerer best som et samarbeidsverktøy, ikke som en fasit. Manuell kvalitetssikring, gjennomgang og refleksjon var avgjørende for å sikre korrekte og relevante resultater. Vi erfarte også at tydelige rammer og gode prompts hadde stor betydning for kvaliteten på svarene.

Samlet sett var KI en netto positiv faktor som forbedret både arbeidsflyt og sluttresultat, men prosjektet understreket viktigheten av å kombinere KI-støtte med menneskelig vurdering og kritisk tenkning.

---

### 5.1 Ansvar og eierskap

Selv om KI bidro i utviklingen, er det fortsatt vi som studenter som har ansvaret for all kode og dokumentasjon i prosjektet. KI fungerer som et støtteverktøy, men kan ikke holdes ansvarlig for kvalitet, riktighet eller konsekvenser av løsningene den foreslår. Det innebærer at vi må forstå, kvalitetssikre og teste alt som genereres før det tas inn i prosjektet. Bruk av KI fritar oss ikke for faglig ansvar, men forutsetter tilstrekkelig innsikt til å vurdere om løsningene faktisk er gode.

Manuell gjennomgang, testing og eventuell refaktorering er nødvendig for å sikre kvalitet i KI-generert kode. Selv om koden kan se riktig ut, kan den inneholde skjulte feil, mangler eller lite forståelige løsninger, noe som gjør kvalitetssikring særlig viktig når KI produserer større kodebolker.

Når det gjelder opphavsrett, regnes prosjektets kode som studentarbeid selv om deler er KI-generert. KI har ingen juridiske rettigheter til innholdet, og institusjonen behandler det som levert av gruppen. Samtidig må man være oppmerksom på at KI kan produsere løsninger som ligner materiale fra åpne databaser eller treningsdata. Derfor er det viktig å sikre at innholdet ikke bryter lisenser eller inkluderer sensitiv informasjon.

### 5.2 Transparens

Det bør være full transparens rundt bruken av KI i et utviklingsprosjekt, særlig i en akademisk kontekst. Åpenhet gjør det mulig for sensor og andre lesere å forstå hvordan arbeidet er utført, og hvilke deler som er generert med KI-støtte. Dette er viktig for å sikre akademisk integritet og for å vise at vi som gruppe forstår materialet og har gjort selvstendige vurderinger.

Dokumentasjon av KI-bidrag innebærer å beskrive hvilke deler av prosessen KI ble brukt i, hvilke typer oppgaver som ble løst med KI-støtte, og hvordan vi kvalitetssikret og bearbeidet svarene. Det er også relevant å forklare hvilke begrensninger vi møtte, og hvordan vi håndterte feil eller misforståelser modellen introduserte.

Manglende transparens kan skape tvil om hvem som står bak arbeidet og om vi har tilstrekkelig forståelse til å forsvare løsningene våre. Det kan også svekke prosjektets troverdighet dersom KI-bruk skjules, og gi inntrykk av at vi forsøker å ta æren for arbeid som ikke er vårt. Derfor er åpenhet nødvendig for en rettferdig og faglig korrekt evaluering.

### 5.3 Påvirkning på læring og kompetanse

Bruken av KI påvirker læring og kompetanse på både positive og utfordrende måter. KI gir rask fremdrift og gjør det mulig å produsere dokumenter, kode og analyser på kort tid, noe som er nyttig i prosjekter med stramme tidsfrister. Samtidig kan denne effektiviteten skape en risiko for overavhengighet dersom KI brukes som første løsning fremfor som støtte, noe som kan svekke den dypere læringen som oppstår når man utforsker problemer selv.

Slik avhengighet kan også hindre utviklingen av enkelte ferdigheter, som å skrive strukturert dokumentasjon fra bunnen av, løse problemer kritisk, kode detaljert uten hjelp og gjennomføre tekniske analyser uten forhåndsgenerte forslag. I tillegg kan man miste forståelsen for underliggende prinsipper dersom KI leverer ferdige svar uten at man selv arbeider seg frem til innsikten.

For å opprettholde balansen mellom effektivitet og læring må KI brukes som et supplement, ikke en erstatning. Vi erfarte at den beste utviklingen oppstod når KI-støtte ble kombinert med egen vurdering, manuell kvalitetssikring og refleksjon over prosessen. Dette gjorde det mulig å dra nytte av KI samtidig som vi utviklet kompetanse som er viktig for videre studier og fremtidig arbeidsliv.

### 5.4 Arbeidsmarkedet

Utbredt bruk av KI vil påvirke fremtidige jobber innen IT og teknologi betydelig. Mange oppgaver som tidligere krevde manuell koding, dokumentasjon eller analyse kan nå automatiseres eller støttes av KI-verktøy. Dette gjør at enkelte tradisjonelle roller, særlig de som omhandler repetitivt eller standardisert arbeid, kan få mindre fokus. Samtidig øker behovet for kompetanse innen KI-integrasjon, systemforståelse, datasikkerhet og kvalitetssikring av KI-generert innhold.

Roller som systemarkitekter, KI-eksperter, sikkerhetsspesialister og tekniske prosjektledere vil sannsynligvis bli viktigere, ettersom de krever helhetsforståelse, kritisk tenkning og evne til å kombinere menneskelig vurdering med KI-støtte. Mer rene junior- og kodeproduksjonsroller kan få redusert betydning, siden KI allerede kan generere funksjonell kode raskt. Fremtidens arbeid vil i større grad handle om å forstå, kontrollere og kvalitetssikre systemene fremfor å skrive all koden selv.

For vår egen karriere blir det avgjørende å bruke KI effektivt samtidig som vi utvikler en faglig plattform KI ikke kan erstatte. Jobber i en KI-drevet verden vil kreve teknisk innsikt, kritisk vurderingsevne og forståelse av hvordan KI bør styres og kvalitetssikres. Det viktigste blir å bruke KI som et verktøy—ikke en krykke—og å bygge kompetanse som gjør det mulig å kombinere automatisering med menneskelig ekspertise.

### 5.5 Datasikkerhet og personvern

I prosjektet delte vi hovedsakelig tekniske beskrivelser, kodeutkast og BMAD-relaterte dokumenter med KI-verktøyene. Vi unngikk bevisst sensitiv informasjon, personopplysninger og data som kunne knyttes til enkeltpersoner, ettersom KI-modeller behandler innhold midlertidig og det ikke alltid er full transparens rundt intern databruk.

Det finnes reelle risikoer ved å dele kode og prosjektdata med KI. Man kan utilsiktet dele proprietær informasjon, og KI kan generere forslag påvirket av lisensbelagt materiale fra treningsdata. Det er også en risiko for at modeller kan gjenspeile mønstre fra annet brukerinnhold, selv om moderne systemer reduserer dette.

Når man bruker KI, bør den behandles som en ekstern tjeneste: del kun det som er nødvendig, unngå sensitivt innhold og sørg for at alt som sendes til KI kunne vært delt offentlig. All KI-generert kode må kvalitetssikres for å unngå sikkerhetshull eller utrygge løsninger. En kritisk og bevisst tilnærming er nødvendig for å kombinere effektiv KI-bruk med ansvarlig databehandling.

---

### 6.1 Kodekvalitet og vedlikehold

KI-generert kode kan være effektiv i starten av et prosjekt, men den skaper utfordringer for langsiktig vedlikehold. Selv om koden som produseres ofte fungerer, er den ikke alltid skrevet med tanke på struktur, lesbarhet eller beste praksis. Dette kan gjøre det vanskeligere å forstå og videreutvikle den senere. KI genererer løsninger som fremstår logiske for modellen, men som ikke nødvendigvis følger et konsistent mønster som er lett for mennesker å arbeide videre med.

Når det gjelder forståelighet, opplevde vi at KI-kode tidvis var godt strukturert, men like ofte for kompakt, unødvendig kompleks eller uten forklarende kommentarer. Dette skaper ekstra arbeid for utviklere som senere skal lese og bruke koden. Derfor blir det nødvendig å rydde opp, kommentere og gjøre koden mer pedagogisk før den tas videre i prosjektet.

Debugging av KI-generert kode kan også være utfordrende. KI kan produsere kode som ser korrekt ut, men som skjuler små logiske feil eller avvik fra kravene. Siden modellen ikke alltid følger menneskelig tankegang i utformingen, kan det være vanskelig å identifisere hva som gikk galt. Dette kan føre til mer tid brukt på feilsøking enn om man hadde skrevet koden selv. Erfaringen vår var at KI fungerer godt for å produsere utkast, men at kvalitet og vedlikehold krever grundig manuell oppfølging.


### 6.2 Standarder og beste praksis

KI følger ikke alltid beste praksis eller etablerte industristandarder. Selv om løsninger ofte fungerer teknisk, kan de være unødvendig komplekse, mindre sikre eller basert på rammeverk og mønstre som ikke lenger anbefales. Dette skyldes at KI trenes på store mengder historisk data, som også inneholder utdaterte eller suboptimale eksempler.

I prosjektet opplevde vi flere tilfeller der KI foreslo lite hensiktsmessige løsninger eller ikke fulgte BMAD-rammeverket som forventet. Noen ganger genererte den også kode som ikke harmonerte med moderne praksis innen rammeverkene vi brukte. Selv om forslagene ga et utgangspunkt, krevde de ofte manuell redesign eller forenkling.

Dette understreker viktigheten av å validere alle KI-forslag før de tas inn i prosjektet. KI er et kraftig støtteverktøy, men det forutsetter at utviklere har nok forståelse til å vurdere hva som faktisk er riktig og fremtidsrettet. Kritisk gjennomgang, sammenligning med oppdaterte kilder og kvalitetssikring er avgjørende for å sikre god teknisk standard.


### 6.3 Fremtidig utvikling

Vi tror KI vil få en stadig større rolle i programvareutvikling. Mange oppgaver som tidligere krevde mye tid—som dokumentasjon, kodeutkast, testing og feilsøking—kan delvis automatiseres eller støttes av KI. Utviklere vil i økende grad fungere som arkitekter og kvalitetskontrollører som styrer prosessen, vurderer løsninger og sikrer at systemene følger krav og standarder. KI vil ikke erstatte utviklere, men den vil endre arbeidsmetoder og hvilke oppgaver som krever manuell innsats.

Dette innebærer at nye ferdigheter blir viktige. Kritisk tenkning, systemforståelse og evnen til å evaluere KI-generert innhold vil stå sentralt. Samarbeid mellom mennesker og KI blir en kjernekompetanse, der prompt engineering og evnen til å formulere presise instruksjoner blir naturlige ferdigheter. Samtidig forblir klassiske disipliner som feilsøking, sikkerhet og arkitektur avgjørende for å sikre kvalitet og robusthet i løsninger der KI bidrar.

Basert på våre erfaringer bør KI brukes bevisst og strukturert. Den bør fungere som et supplement som sparer tid og gir forslag, men ikke som en erstatning for egen vurdering eller faglig forståelse. Alle KI-forslag må kvalitetssikres, forbedres og tilpasses av mennesker. Med riktig bruk kan KI gi betydelig verdi, men dette krever en aktiv, kritisk og ansvarlig utviklingspraksis.

---

### 7.1 Viktigste lærdommer

1. **Bruk av KI som utviklingsverktøy:**  
   Vi lærte hvordan KI kan brukes effektivt som støtte i planlegging, dokumentasjon og koding. Prosjektet ga erfaring i å formulere presise prompts, styre KI i riktig retning og bruke den som en samarbeidspartner i utviklingsprosessen.

2. **Forståelse av utviklingsprosessen:**  
   Vi fikk bedre innsikt i hvordan en strukturert utviklingsprosess fungerer gjennom bruken av BMAD-metodikken. Dette gjorde oss mer bevisste på sammenhengen mellom behov, mål, arkitektur og implementasjon.

3. **Forståelse av begrensningene til KI:**  
   Vi erfarte at KI ikke alltid leverer korrekte eller relevante svar, og at det derfor er nødvendig å forstå modellens begrensninger. Dette ga oss bedre grunnlag for å vite når vi kan stole på KI og når vi må være ekstra kritiske.

4. **Viktigheten av overordnet faglig forståelse:**  
   Prosjektet viste at man ikke trenger å kunne alle tekniske detaljer i dybden for å jobbe effektivt, så lenge man har en god overordnet forståelse. Ved å forstå prinsipper, struktur og mål kunne vi bruke KI til å fylle inn detaljer uten å miste kontroll over helheten.

5. **Bedre samarbeid gjennom tydelig kommunikasjon:**  
   Prosjektet understreket viktigheten av tydelig og kontinuerlig kommunikasjon, spesielt i digitalt og asynkront arbeid. Klare forventninger, statusoppdateringer og aktiv bruk av Teams og Messenger bidro til bedre koordinering og færre misforståelser.


### 7.2 Hva ville dere gjort annerledes?

Når det gjelder KI-bruken, ville vi vært mer bevisste fra starten på hvordan vi formulerte prompts og styrte modellen. Vi erfarte at kvaliteten på KI-svarene var sterkt avhengig av presise og konkrete instruksjoner. Med tydeligere retningslinjer tidlig i prosjektet kunne vi unngått flere av feilene som gjorde at deler av BMAD-prosessen måtte startes på nytt.

I samarbeid og organisering ville vi etablert en mer strukturert plan for kommunikasjon, rollefordeling og oppfølging. Selv om samarbeidet fungerte godt, kunne hyppigere statusmøter og tydeligere arbeidsfordeling gjort fremdriften jevnere og redusert behovet for løpende avklaringer.

Samlet sett ville disse endringene gitt en mer effektiv prosess og et bedre sluttresultat, samtidig som arbeidet kunne blitt mer systematisk og forutsigbart gjennom hele prosjektet.

### 7.3 Anbefalinger

Vår hovedanbefaling til andre studenter som skal bruke KI i utviklingsprosjekter, er å være tydelige og presise når dere formulerer instrukser. God promptskriving er avgjørende for å få nyttige og konsistente svar. Bruk gjerne KI til å generere utkast, ideer og struktur, men sørg for å revidere og kvalitetssikre alt før det tas i bruk. KI fungerer best som støtte, ikke som fasit.

En viktig fallgruve er å bli for avhengig av KI. Det kan være fristende å la modellen løse alt, men dette kan hemme læringen og føre til redusert oversikt over prosjektet. KI kan gi feil svar, misforstå oppgaven eller bevege seg i uventede retninger. Når dette skjer, er det ofte bedre å starte en ny samtale enn å fortsette en tråd som allerede har gått seg fast.

Som beste praksis anbefaler vi å lagre gode prompts underveis, jobbe med korte og avgrensede spørsmål, og alltid kombinere KI-forslag med egen faglig vurdering. Hyppig bruk av `commit` og `git pull` i GitHub bidrar også til bedre samarbeid og kontroll. KI kan gi stor verdi i utviklingsprosjekter, så lenge

### 7.4 Personlig refleksjon (individuelt)

**[Navn på gruppemedlem 1]:**
[Personlig refleksjon over egen læring og utvikling]

**[Navn på gruppemedlem 2]:**
[Personlig refleksjon over egen læring og utvikling]

**[Navn på gruppemedlem 3]:**
[Personlig refleksjon over egen læring og utvikling]

---

## 8. Vedlegg (valgfritt)

- Skjermbilder av applikasjonen
- Lenke til GitHub repository
- Annen relevant dokumentasjon

---

**Ordantall:** [Ca. antall ord]

**Forventet lengde:** 3000-5000 ord (avhengig av gruppestørrelse og prosjektets kompleksitet)