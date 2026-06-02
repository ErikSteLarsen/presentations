<span class="kicker">AI-assistert kode · Kapittel 6 & 7</span>

# Tillit gjennom struktur

Verifisering og beste praksis

Fra «vibe coding» til verifisert, skalerbar utvikling

Erik

<div class="bv-scene bv-center"><svg class="bv-fig" style="width:170px"><use href="#bv-hills"/></svg><svg class="bv-fig" style="width:120px"><use href="#bv-tree"/></svg></div>

Note: Velkommen. Denne presentasjonen handler om hvordan vi går fra å håpe at AI-generert kode er riktig, til å vite det. Vi bygger på kapittel 6 og 7 i RPI-metoden — Research, Plan, Implement. Målet er tillit gjennom struktur, ikke blind tro.

---

<span class="kicker">Agenda</span>

## Hva vi skal gjennom

<div class="cards two">
<div class="card">

#### Del 1 — Verifisering og tillit

Hvorfor vi ikke kan stole blindt på AI-kode, og hvordan vi bygger berettiget tillit gjennom lagdelt verifisering.

</div>
<div class="card">

#### Del 2 — Beste praksis

Konkrete oppskrifter, de ti bud, erfaringer fra reelle prosjekter, og et veikart for å komme i gang.

</div>
</div>

**Mål:** konkrete vaner du kan ta i bruk fra dag én.

Note: To deler. Først det teoretiske fundamentet for verifisering og tillit, deretter den praktiske anvendelsen. Poenget er ikke abstrakte prinsipper, men vaner du kan ta i bruk umiddelbart.

---

<!-- .slide: class="section-header" data-background-gradient="linear-gradient(150deg, #eaf0f4 0%, #f0e4cc 100%)" -->

## Del 1 · Verifisering og tillit

<div class="bv-scene bv-center"><svg class="bv-fig" style="width:150px"><use href="#bv-explorer"/></svg><svg class="bv-fig" style="width:120px"><use href="#bv-leaf"/></svg></div>

Note: Vi starter med det grunnleggende spørsmålet — hvordan kan vi stole på kode vi ikke har skrevet selv?

---

<span class="kicker">Del 1 · Hvorfor verifisere</span>

## Hvorfor verifisering er kritisk

<div class="stats">
<div class="stat"><span class="num">5×</span><span class="label">mer kode</span></div>
<div class="stat"><span class="num">5×</span><span class="label">flere bugs</span></div>
<div class="stat"><span class="num">5×</span><span class="label">mer risiko</span></div>
</div>

- 5× mer kode betyr 5× mer vedlikehold og 5× mer som kan gå galt
- Verifisering går fra «best practice» til **overlevelseskritisk**
- Kjernebudskap: tillit gjennom struktur, ikke blind tro

<div class="bv-corner bv-br bv-sm"><svg class="bv-fig"><use href="#bv-computer"/></svg></div>

Note: Når AI lar oss produsere mange ganger mer kode, skalerer ikke bare produktiviteten — også risikoen og vedlikeholdsbyrden vokser tilsvarende. Det som før var en god vane blir nå avgjørende for å overleve. Hele resten av presentasjonen bygger på dette ene poenget.

---

<span class="kicker">Del 1 · Tillitsunderskuddet</span>

## Tillitsunderskuddet

<div class="stats">
<div class="stat"><span class="num">82 %</span><span class="label">bruker AI-assistenter</span></div>
<div class="stat"><span class="num">76 %</span><span class="label">stoler ikke på outputen</span></div>
</div>

- Et **rasjonelt** underskudd — skepsis er sunt
- Hovedårsak: «vi stoler ikke på konteksten modellen har»
- Underskuddet forsvinner ikke av seg selv — det må bygges ned med struktur

<div class="bv-corner bv-br"><svg class="bv-fig"><use href="#bv-ideate"/></svg></div>

Note: De fleste bruker AI, men de fleste stoler ikke på resultatet. Det er ikke irrasjonelt — det er sunn skepsis. Kjernen er at modellen ofte mangler full kontekst om prosjektet vårt. Løsningen er ikke mer blind tro, men strukturer som gjør tilliten berettiget.

---

<span class="kicker">Del 1 · Feilmodi</span>

## Hvorfor AI-kode feiler

<div class="cards two">
<div class="card">

#### Subtile feil

Kompilerer og ser riktig ut, men feiler under spesifikke forhold.

</div>
<div class="card">

#### Sikkerhetshull

Gjenskaper usikre mønstre fra treningsdataene.

</div>
<div class="card">

#### Arkitektonisk inkoherens

Bryter prosjektets etablerte mønstre.

</div>
<div class="card">

#### Utelatelser

Glemmer edge cases du ikke nevnte.

</div>
</div>

Poenget er ikke å slutte med AI — men å bygge tillit som er *berettiget*.

Note: AI-kode feiler på måter som er vanskeligere å oppdage enn vanlige feil, fordi den ofte ser helt riktig ut. Den kan gjenskape usikre mønstre, bryte arkitekturen din, eller glemme tilfeller du ikke eksplisitt nevnte. Konklusjonen er ikke å unngå AI, men å verifisere systematisk.

---

<span class="kicker">Del 1 · Verifiseringspyramiden</span>

## Verifiseringspyramiden

<div class="pyramid">
<div class="tier t1">E2E-tester</div>
<div class="tier t2">Integrasjonstester</div>
<div class="tier t3">Enhetstester</div>
<div class="tier t4">Statisk analyse</div>
<div class="tier t5">Kode- & plangjennomgang</div>
</div>

Lag på lag av forsvar — fra rask, automatisk sjekk nederst til menneskelig vurdering på toppen.

Note: Tenk på verifisering som en pyramide. Nederst ligger den brede, billige og automatiske foundasjonen — statisk analyse og gjennomgang. Jo høyere opp, jo nærmere den fullstendige brukeropplevelsen kommer vi, men også tregere og dyrere. Ingen enkelt lag er nok alene.

---

<span class="kicker">Del 1 · Lag 1/5 · Fundamentet</span>

## Kode- & plangjennomgang

<p class="lead">Menneskelig vurdering — fanger feilene maskiner ikke ser.</p>

- **Fanger:** feil arkitektur, feil tilnærming, manglende krav
- **Eksempel:** koden er feilfri, men løser feil problem
- Billigst å rette her — før en eneste linje er skrevet

<div class="pyramid bv-mini">
<div class="tier t1 dim">E2E-tester</div>
<div class="tier t2 dim">Integrasjonstester</div>
<div class="tier t3 dim">Enhetstester</div>
<div class="tier t4 dim">Statisk analyse</div>
<div class="tier t5">Kode- & plangjennomgang</div>
</div>

Note: Fundamentet i pyramiden er menneskelig gjennomgang av plan og kode. Dette laget fanger de dyreste feilene — feil arkitektur eller feil tilnærming — som ingen test ville oppdaget, fordi koden teknisk sett kan være perfekt. Retter du det på plan-stadiet, sparer du mest.

---

<span class="kicker">Del 1 · Lag 2/5 · Automatisk</span>

## Statisk analyse

<p class="lead">Kompilatoren og linteren — lynrask og helautomatisk.</p>

- **Fanger:** syntaks-, type- og stilfeil
- **Eksempel:** `user.nmae` i stedet for `user.name`
- Kjører på millisekunder, uten å starte koden

<div class="pyramid bv-mini">
<div class="tier t1 dim">E2E-tester</div>
<div class="tier t2 dim">Integrasjonstester</div>
<div class="tier t3 dim">Enhetstester</div>
<div class="tier t4">Statisk analyse</div>
<div class="tier t5 dim">Kode- & plangjennomgang</div>
</div>

Note: Statisk analyse — TypeScript og lint — er det raskeste laget. Det fanger skrivefeil og typefeil før koden i det hele tatt kjøres, på millisekunder. Billig, automatisk og alltid på.

---

<span class="kicker">Del 1 · Lag 3/5 · Logikk</span>

## Enhetstester

<p class="lead">Verifiserer at enkeltfunksjoner gjør det de skal.</p>

- **Fanger:** logiske feil i isolerte funksjoner
- **Eksempel:** en skatteberegning som gir feil sum
- Raske og presise — peker rett på hva som feiler

<div class="pyramid bv-mini">
<div class="tier t1 dim">E2E-tester</div>
<div class="tier t2 dim">Integrasjonstester</div>
<div class="tier t3">Enhetstester</div>
<div class="tier t4 dim">Statisk analyse</div>
<div class="tier t5 dim">Kode- & plangjennomgang</div>
</div>

Note: Enhetstester sjekker logikken i enkeltfunksjoner isolert. Når en feiler, vet du nøyaktig hvor problemet er. Raske å kjøre og presise i diagnosen — ryggraden i en god testsuite.

---

<span class="kicker">Del 1 · Lag 4/5 · Samspill</span>

## Integrasjonstester

<p class="lead">Sjekker at delene fungerer sammen, ikke bare hver for seg.</p>

- **Fanger:** feil i samspillet mellom komponenter
- **Eksempel:** API-et leverer data, men frontend viser den ikke
- Hver del kan være riktig — likevel knirker koblingen

<div class="pyramid bv-mini">
<div class="tier t1 dim">E2E-tester</div>
<div class="tier t2">Integrasjonstester</div>
<div class="tier t3 dim">Enhetstester</div>
<div class="tier t4 dim">Statisk analyse</div>
<div class="tier t5 dim">Kode- & plangjennomgang</div>
</div>

Note: Integrasjonstester fanger feil som oppstår i koblingen mellom komponenter — der hver del fungerer alene, men ikke sammen. Et klassisk eksempel er at API-et returnerer riktig data, men frontend tolker eller viser den feil.

---

<span class="kicker">Del 1 · Lag 5/5 · Toppen</span>

## E2E-tester

<p class="lead">Følger hele brukerflyten — nærmest ekte bruk.</p>

- **Fanger:** brudd i den faktiske brukeropplevelsen
- **Eksempel:** brukeren får ikke fullført checkout
- Bredest dekning, men tregest og vagest på årsak

<div class="pyramid bv-mini">
<div class="tier t1">E2E-tester</div>
<div class="tier t2 dim">Integrasjonstester</div>
<div class="tier t3 dim">Enhetstester</div>
<div class="tier t4 dim">Statisk analyse</div>
<div class="tier t5 dim">Kode- & plangjennomgang</div>
</div>

Note: E2E-tester kjører hele flyten slik en bruker opplever den. De fanger at alt henger sammen ende-til-ende, men er tregere og sier mindre om hvor feilen ligger. Derfor toppen av pyramiden — verdifullt, men ikke noe du baserer alt på.

---

<span class="kicker">Del 1 · Visuell verifisering</span>

## Visuell verifisering med Playwright

<div class="flow">
<div class="step">Last side</div>
<div class="step">Sjekk console-feil</div>
<div class="step">Ta screenshot</div>
<div class="step">Verifiser elementer</div>
</div>

- Frontend kan kompilere og passere enhetstester — og likevel se helt feil ut
- **Obligatorisk** for frontend-oppgaver
- Visuell regresjon mot baseline fanger ødelagt layout

<div class="bv-corner bv-bl"><svg class="bv-fig"><use href="#bv-explorer"/></svg></div>

Note: Et naturlig tillegg på toppen av testlagene, spesielt for frontend: koden kan kompilere og passere enhetstester og likevel se helt feil ut. Derfor er visuell verifisering obligatorisk for frontend — last siden, sjekk for console-feil, ta et screenshot og verifiser at kritiske elementer er på plass. Visuell regresjon mot en baseline fanger layout som har knekt.

---

<span class="kicker">Del 1 · CI/CD</span>

## CI/CD i AI-æraen

<div class="flow">
<div class="step">TypeScript<br><strong>2 s</strong></div>
<div class="step">Lint<br><strong>3 s</strong></div>
<div class="step">Enhetstester<br><strong>10 s</strong></div>
<div class="step">Integrasjon<br><strong>1 min</strong></div>
<div class="step">E2E<br><strong>5 min</strong></div>
</div>

- 5× mer kode krever 5× bedre verifisering — manuell review skalerer ikke
- **Fail fast, fail loud:** kjør de billigste sjekkene først
- Feil oppdaget tidlig = rask, billig tilbakemelding

Note: Manuell gjennomgang skalerer ikke når kodemengden femdobles — pipelines gjør det. Nøkkelprinsippet er fail fast: kjør de raskeste og billigste sjekkene først, så en typefeil stopper deg etter to sekunder i stedet for fem minutter. Tidlig feil betyr rask feedback.

---

<span class="kicker">Del 1 · Pre-commit hooks</span>

## Pre-commit hooks

- Kjør **typecheck + lint før** commit — ikke etter push
- Fang trivielle feil lokalt, på sekunder
- Enda kortere feedback-løkke enn CI/CD alene
- CI/CD blir sikkerhetsnettet, ikke førstelinjen

<div class="bv-corner bv-br"><svg class="bv-fig"><use href="#bv-test"/></svg></div>

Note: Pre-commit hooks flytter de raskeste sjekkene helt frem til commit-øyeblikket. Du fanger trivielle feil før de i det hele tatt når repoet. Det gir den korteste mulige feedback-løkken, og lar CI/CD være sikkerhetsnettet i stedet for førstelinjeforsvaret.

---

<span class="kicker">Del 1 · TDD med AI</span>

## Test-drevet AI-utvikling

<div class="flow">
<div class="step"><strong>DU</strong><br>skriver test<br>(feiler)</div>
<div class="step"><strong>AI</strong><br>skriver kode<br>(passerer)</div>
<div class="step"><strong>DU</strong><br>verifiserer &amp;<br>refaktorerer</div>
</div>

- Testen er et **konkret mål** AI-en skal treffe — verifiser, ikke håp
- Testen er **entydig kommunikasjon** — bedre enn «håndter edge cases» i prosa

Note: TDD snur arbeidsflyten: du skriver testen som feiler, AI skriver koden som får den til å passere, og du verifiserer og refaktorerer. Testen blir både et konkret, målbart mål og en entydig spesifikasjon. Det er langt mer presist enn å be om at AI «håndterer edge cases» i fritekst.

---

<span class="kicker">Del 1 · Plan vs. kode</span>

## Plangjennomgang over kodegjennomgang

<div class="cards two">
<div class="card">

#### Tradisjonelt: kodegjennomgang

Les 500+ linjer kode. Timer eller dager per review. Dyrt å snu retning når koden allerede er skrevet.

</div>
<div class="card">

#### Med RPI + AI: plangjennomgang

Gjennomgå ~50 linjer plan. Minutter per review. Fanger feil arkitektur, feil tilnærming og manglende krav — før koden finnes.

</div>
</div>

Verifiser at tilnærmingen er arkitektonisk sunn; la CI/CD ta detaljene.

Note: Tradisjonell kodegjennomgang betyr å lese hundrevis av linjer, ofte når det er for sent å snu. Med RPI gjennomgår du i stedet en kort plan på rundt femti linjer. Du fanger de dyre feilene — feil arkitektur eller tilnærming — på minutter, før en eneste linje kode er skrevet.

---

<span class="kicker">Del 1 · Konklusjon</span>

## Tillit gjennom struktur

<div class="contrast">
<div class="panel from">

#### Blind tillit

«AI-en vet best» → bugs, sikkerhetshull, teknisk gjeld → mistillit over tid.

</div>
<div class="arrow">→</div>
<div class="panel to">

#### Verifisert tillit

«AI-en har bevist det» → tester grønne, CI/CD grønn, plan godkjent → tillit som vokser.

</div>
</div>

> «Trust in AI isn't about faith. It's about verification.»

Note: Kontrasten er kjernen i hele del 1. Blind tillit fører til en nedadgående spiral av teknisk gjeld og mistillit. Verifisert tillit vokser, fordi den bygger på bevis. Utviklerens nye jobb er å definere suksess, gjennomgå planer, bygge pipelines og verifisere output — ikke å skrive hver linje selv.

---

<span class="kicker">Del 1 · Oppsummering</span>

## Nøkkelpunkter — Del 1

- **Tillitsunderskuddet:** 76 % stoler ikke på AI — og det er rasjonelt
- **Verifiseringspyramiden:** lag på lag av forsvar
- **CI/CD er kritisk:** automatiser og fail fast
- **TDD med AI:** du skriver testene, AI implementerer
- **Plangjennomgang:** 50 linjer plan > 500 linjer kode

Note: Oppsummert: skepsis er rasjonelt, og svaret er lagdelt verifisering. Automatiser med CI/CD, snu arbeidsflyten med TDD, og flytt gjennomgangen fra kode til plan. Dette er fundamentet vi bygger den praktiske delen på.

---

<!-- .slide: class="section-header" data-background-gradient="linear-gradient(150deg, #eaf0f4 0%, #f0e4cc 100%)" -->

## Del 2 · Beste praksis og praktisk anvendelse

<div class="bv-scene bv-center"><svg class="bv-fig" style="width:160px"><use href="#bv-mountain"/></svg><svg class="bv-fig" style="width:120px"><use href="#bv-hills"/></svg></div>

Note: Nå som vi vet hvordan vi verifiserer, ser vi på de overordnede prinsippene og hvordan du faktisk kommer i gang.

---

<span class="kicker">Del 2 · Fra teori til praksis</span>

## Fra teori til praksis

<p class="lead">Ikke en ferdig fasit — «beste praksis» endrer seg ekstremt fort.</p>

- Kjenn fundamentet — så kan teamet velge hvordan dere tilpasser AI best
- Kjenner du «beste praksis», er det lettere å henge med videre

<div class="bv-corner bv-br"><svg class="bv-fig"><use href="#bv-mountain"/></svg></div>

Note: Beste praksis for AI-utvikling er et bevegelig mål — det som gjelder i dag, kan være forandret om noen måneder. Derfor er ikke dette en fasit. Men kjenner du fundamentet, kan teamet ditt selv vurdere hvordan dere bør tilpasse bruken av AI til akkurat dere. Og kjenner du gårsdagens beste praksis, er det mye lettere å henge med på utviklingen videre. Vi starter med et av fundamentene: compounding engineering.

---

<span class="kicker">Del 2 · Compounding engineering</span>

## Compounding engineering

<p class="lead">Investeringer i utviklingsprosessen som gir utbytte over tid.</p>

- Ikke engangsforbedringer — **systemer som blir bedre jo mer du bruker dem**
- Analogi: rentes rente, men for utviklingspraksis
- Hver forbedring gjør neste AI-interaksjon bedre

<div class="bv-corner bv-br"><svg class="bv-fig"><use href="#bv-shapes"/></svg></div>

Note: Compounding engineering er at investeringer i prosessen forrenter seg. En god testsuite gjør AI-kode bedre, som gjør utvikling raskere, som frigjør tid til å forbedre testsuiten ytterligere. Det er rentes rente for utviklingspraksis — en positiv spiral.

---

<span class="kicker">Del 2 · Compounding i praksis</span>

## Compounding i praksis

<div class="cards two">
<div class="card">

#### Domeneminne

Skriv `auth.md` én gang → spar timevis med gjentatt forklaring senere.

</div>
<div class="card">

#### Test-suite

En investering som fanger stadig flere bugs over tid.

</div>
<div class="card">

#### Delt domenespråk

En levende ordliste over domenebegrepene holder AI-ens språk i tråd med vårt — skrevet én gang, brukt overalt.

</div>
<div class="card">

#### Tankesett

Fra «fikset buggen» til «la til en test som forhindrer denne typen bug».

</div>
</div>

Note: Konkret ser compounding slik ut: domeneminne du skriver én gang sparer titalls timer senere, testsuiten fanger stadig mer, og en delt domeneordliste holder AI-ens begreper i tråd med domenet vårt. Det viktigste er tankeskiftet — fra å fikse enkeltbugs til å bygge systemer som forhindrer hele klasser av bugs.

---

<span class="kicker">Del 2 · Forbedringsløkke</span>

## Kontinuerlig forbedringsløkke

<div class="loop">
<div class="node"><span class="n">1</span><p>Gjør oppgave med AI</p></div>
<div class="node"><span class="n">2</span><p>Identifiser friksjon — måtte du forklare flere ganger?</p></div>
<div class="node"><span class="n">4</span><p>Neste oppgave blir lettere → gjenta</p></div>
<div class="node"><span class="n">3</span><p>Dokumentér løsningen — som rule, skill eller test</p></div>
</div>

Dette **er** compounding engineering i praksis. ↻

<div class="bv-corner bv-tr bv-sm"><svg class="bv-fig"><use href="#bv-tree"/></svg></div>

Note: Løkken er enkel: gjør en oppgave, legg merke til friksjonen — måtte du forklare det samme flere ganger? — og dokumentér løsningen som en rule, skill eller test. Neste oppgave blir lettere, og du gjentar. Dette er compounding engineering konkretisert — og broen videre til de ti bud.

---

<span class="kicker">Del 2 · De ti bud (1–5)</span>

## De ti bud

1. **Ikke outsource tenkingen** — AI forsterker, erstatter ikke
2. **Hold konteksten ren** — under 40 %, komprimer, start friskt
3. **Definer suksess før implementering** — tester & akseptansekriterier
4. **Aldri ship uverifisert kode** — AI-kode trenger *mer* verifisering
5. **Gjennomgå planer**, ikke bare kode

Note: De fem første budene handler om disiplin og kvalitetssikring. Du eier tenkingen, du holder konteksten ren, og du definerer hva suksess betyr før AI begynner. Og du sender aldri uverifisert kode — AI-kode trenger mer verifisering, ikke mindre.

---

<span class="kicker">Del 2 · De ti bud (6–10)</span>

## De ti bud (fortsettelse)

<ol start="6">
<li><strong>Bygg domeneminne</strong> — CLAUDE.md, rules-filer, domeneordlister</li>
<li><strong>Bruk RPI religiøst</strong> — Research → Plan → Implement</li>
<li><strong>Ikke frykt nye sesjoner</strong> — god hygiene, ikke fiasko</li>
<li><strong>Invester i compounding</strong> — dokumentér mønstre, bygg systemer</li>
<li><strong>Forbli skeptisk, men pragmatisk</strong> — «trust, but verify»</li>
</ol>

Note: De fem siste handler om systemene rundt arbeidet. Bygg domeneminne, følg RPI konsekvent, og ikke vær redd for å starte friske sesjoner — det er god hygiene. Invester i compounding, og behold den pragmatiske skepsisen: stol, men verifiser.

---

<span class="kicker">Del 2 · Erfaringer fra praksis</span>

## Hva som har fungert for oss

<div class="cards two">
<div class="card">

#### Lav WIP

Hold 1–2 oppgaver in-progress om gangen — kvaliteten faller når for mye skjer parallelt.

</div>
<div class="card">

#### Én kilde, alle verktøy

Samme `AGENTS.md` og skills deles (hardlenket) til Claude, Cursor, Codex og Copilot — reglene vedlikeholdes ett sted.

</div>
<div class="card">

#### Harde regler holder

Eksplisitte «Never Break»-regler blir stort sett respektert — AI bryter dem sjeldnere.

</div>
<div class="card">

#### Konsistens via skills

Samme dokumenterte prosess hver gang har gitt jevnere kvalitet.

</div>
</div>

Note: Dette er erfaringer fra egne prosjekter, ikke en fasit — men noen mønstre har gått igjen. Lav WIP ser ut til å holde kvaliteten oppe, det å dele samme AGENTS.md og skills på tvers av verktøy sparer mye vedlikehold, og eksplisitte «Never Break»-regler blir stort sett respektert. Og en dokumentert prosess via skills har gitt jevnere kvalitet.

---

<span class="kicker">Del 2 · Erfaringer fra praksis</span>

## Det som deles, vokser

<div class="cards two">
<div class="card">

#### Del artefaktene

Rules, skills og planer hører hjemme i git — ikke som private notater. Da eier teamet dem sammen, de kan reviewes, og forbedringer kommer alle til gode.

</div>
<div class="card">

#### Onboarding-gevinst

Det samme domeneminnet som hjelper AI, har også hjulpet nye folk i gang raskere — konteksten ligger allerede skrevet ned.

</div>
</div>

<p class="lead">Vår erfaring: jo mer vi la i felles filer, jo mindre måtte vi forklare på nytt.</p>

<div class="bv-corner bv-tr bv-sm"><svg class="bv-fig"><use href="#bv-book"/></svg></div>

Note: To ting vi ikke så komme i starten. For det første at artefaktene — rules, skills, planer — blir mye mer verdt når de deles i git enn når de ligger lokalt hos én person: teamet eier dem sammen og kan forbedre dem. For det andre at den samme dokumentasjonen som gjør AI bedre, også korter ned onboarding for nye folk. Det er ikke fasit, men det har vært vår erfaring at delt kontekst lønner seg.

---

<span class="kicker">Del 2 · Erfaringer fra praksis</span>

## Lærdommer

<div class="cards">
<div class="card">

#### Repo-script, ikke rå verktøy

Gi AI ett stabilt grensesnitt — `pnpm check`, `pnpm test` — i stedet for rå verktøy som `tsc` eller `eslint` direkte. Skriptet kapsler inn riktige flagg og stier.

</div>
<div class="card">

#### Et rydde-pass før du er ferdig

Når koden virker: forenkle først, så luk bort AI-typisk støy — døde sjekker, defensiv kode, støyende kommentarer.

</div>
<div class="card">

#### Ikke dokumentér alt

Vi `.md`-dokumenterer ikke hver komponent — mye å vedlikeholde, og glemte oppdateringer blir fort til feil.

</div>
</div>

<div class="bv-corner bv-br bv-sm"><svg class="bv-fig"><use href="#bv-test"/></svg></div>

Note: Tre lærdommer fra praksis. Den første: la AI kjøre repo-scriptene — pnpm check, pnpm test — i stedet for de underliggende «rå» verktøyene direkte, som tsc eller eslint. Skriptet vet allerede riktige flagg og stier, så hver kjøring blir lik. Den andre: legg inn et fast rydde-pass etter at koden virker — først forenkle, så luke bort typisk AI-«slop». Og den tredje, motsatt vei: ikke dokumentér alt i .md-filer — det blir mye å vedlikeholde, og en glemt oppdatering gjør fort at dokumentasjonen lyver.

---

<span class="kicker">Del 2 · Vanlige feil</span>

## Vanlige feil → løsning

| Symptom | Løsning |
|---|---|
| For lange sesjoner | Korte sesjoner, progress-filer (< 40 %) |
| Manglende domeneminne | CLAUDE.md + rules |
| Hoppe over planlegging | Bruk RPI, review planer |
| Blind tillit | CI/CD, TDD, code review |
| For mange tools / MCP | Minimalisme |
| Monolittiske oppgaver | Bryt ned i atomiske oppgaver |
| Ingen test-strategi | TDD, coverage-mål, E2E for kritiske flyter |
| Rå verktøy-kommandoer feiler | Repo-script: `pnpm check`, `pnpm test` |
| AI-«slop» blir liggende | Rydde-pass: forenkle, så luk bort støy |

Note: De fleste problemer har et kjent motgift. Lange sesjoner løses med progress-filer og 40 %-regelen, blind tillit med CI/CD og TDD, og monolittiske oppgaver med nedbryting i atomiske biter. Kjenner du symptomet, kjenner du løsningen.

---

<span class="kicker">Del 2 · Kom i gang</span>

## Kom i gang i dag

<div class="timeline">
<div class="stage"><span class="dot"></span><h4>Dag 1</h4><p>CLAUDE.md: stack, kritiske regler, kommandoer</p></div>
<div class="stage"><span class="dot"></span><h4>Uke 1</h4><p>Din første rules-fil</p></div>
<div class="stage"><span class="dot"></span><h4>Måned 1</h4><p>Delt domeneordliste (CONTEXT.md)</p></div>
<div class="stage"><span class="dot"></span><h4>Kvartalet</h4><p>Dokumentér en arbeidsflyt som en skill</p></div>
</div>

Du trenger ikke alt fra dag én — bygg det opp gradvis.

<div class="bv-corner bv-tr bv-sm"><svg class="bv-fig"><use href="#bv-plant"/></svg></div>

Note: Modningskurven er bevisst overkommelig. Dag én lager du en CLAUDE.md. I løpet av uka din første rules-fil. I løpet av måneden en delt domeneordliste, og i løpet av kvartalet dokumenterer du en arbeidsflyt som en skill. Du trenger ikke alt på en gang.

---

<span class="kicker">Del 2 · Transformasjonsreisen</span>

## Transformasjonsreisen

<div class="contrast">
<div class="panel from">

#### Fra

- «Vibe coding»
- Blind tillit
- Hver sesjon fra null
- Kaotisk kontekst
- Manuell review
- Engangsløsninger

</div>
<div class="arrow">→</div>
<div class="panel to">

#### Til

- Strukturert RPI
- Verifisert tillit
- Domeneminne
- 40 %-regelen
- CI/CD + plangjennomgang
- Compounding engineering

</div>
</div>

Note: Dette er reisen samlet på ett bilde. Fra vibe coding til strukturert RPI, fra blind til verifisert tillit, fra kaos til disiplin, fra engangsløsninger til systemer som forrenter seg. Det er ikke seks separate endringer, men én sammenhengende modning.

---

<!-- .slide: class="closing" -->

## Kort oppsummert

Verifiser og standardiser. Invester i prosessen.

Takk for oss! Spørsmål?

<div class="bv-scene bv-center"><svg class="bv-fig" style="width:170px"><use href="#bv-mountain"/></svg><svg class="bv-fig" style="width:130px"><use href="#bv-hills"/></svg></div>

Note: Kort oppsummert: verifiser og standardiser arbeidet, og invester i prosessen så den forrenter seg over tid. Det er det som skiller akselerasjon fra teknisk gjeld. Takk for oppmerksomheten; jeg åpner for spørsmål.
