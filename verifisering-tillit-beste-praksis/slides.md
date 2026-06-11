<span class="kicker">AI-assistert kode · Kapittel 6 & 7</span>

# Tillit gjennom struktur

Verifisering og beste praksis

Fra «vibe coding» til verifisert, skalerbar utvikling

Erik

<div class="bv-scene bv-center"><svg class="bv-fig" style="width:170px"><use href="#bv-hills"/></svg><svg class="bv-fig" style="width:120px"><use href="#bv-tree"/></svg></div>

Note: Velkommen! Kort om hva dette handler om: hvordan vi går fra å håpe at AI-generert kode er riktig, til å faktisk vite det. Jeg bygger på kapittel 6 og 7 fra RPI-metoden — Research, Plan, Implement. Den røde tråden gjennom alt sammen er tittelen: tillit gjennom struktur, ikke blind tro.

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

**Mål:** konkrete vaner og struktur du kan ta i bruk fra dag én.

Note: Vi går gjennom to deler. Først bygger vi det teoretiske fundamentet — verifisering og tillit. Så går vi over på det praktiske: konkrete oppskrifter, de ti bud, erfaringer fra reelle prosjekter og et veikart for å komme i gang. Det viktigste for meg er at dere går herfra med vaner dere kan ta i bruk allerede fra dag én, ikke bare abstrakte prinsipper.

---

<!-- .slide: class="section-header" data-background-gradient="linear-gradient(150deg, #eaf0f4 0%, #f0e4cc 100%)" -->

## Del 1 · Verifisering og tillit

<div class="bv-scene bv-center"><svg class="bv-fig" style="width:150px"><use href="#bv-explorer"/></svg><svg class="bv-fig" style="width:120px"><use href="#bv-leaf"/></svg></div>

Note: Vi starter med det helt grunnleggende spørsmålet: hvordan kan vi stole på kode vi ikke har skrevet selv?

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

Note: Poenget her er enkelt: når AI lar oss lage mange ganger så mye kode, skalerer ikke bare produktiviteten — også risikoen og vedlikeholdsbyrden vokser like mye. Fem ganger mer kode betyr fem ganger mer som kan gå galt. Det som før var en god vane, blir nå kritisk for å overleve. Hele resten av presentasjonen henger på dette ene poenget.

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

Note: Tallene forteller en interessant historie: de aller fleste bruker AI, men nesten like mange stoler ikke på det de får ut. Og det er faktisk ikke irrasjonelt — det er sunn skepsis. Hovedårsaken er at modellen ofte mangler full kontekst om akkurat vårt prosjekt. Svaret er ikke mer blind tro, men strukturer som gjør tilliten berettiget — for dette underskuddet forsvinner ikke av seg selv.

---

<span class="kicker">Del 1 · Feilmodi</span>

## Hvorfor AI-kode feiler

<div class="cards two">
<div class="card">

#### Subtile feil / Edge cases

Kompilerer og ser riktig ut, men feiler under forhold du ikke nevnte.

</div>
<div class="card">

#### Sikkerhetshull

Gjenskaper usikre mønstre fra treningsdataene.

</div>
<div class="card">

#### Feil mønstre

Bruker utdaterte mønstre og bryter prosjektets konvensjoner — fordi den ikke kjenner hele kodebasen din.

</div>
<div class="card">

#### Overkomplisering

Legger til abstraksjoner og kode du ikke ba om.

</div>
</div>

Poenget er ikke å slutte med AI — men å bygge tillit som er *berettiget*.

Note: AI-kode feiler på måter som er vanskeligere å oppdage enn vanlige feil, nettopp fordi den ofte ser helt riktig ut. Fire typiske feilmodi: subtile feil og edge cases du ikke nevnte, sikkerhetshull den har lært fra treningsdataene, feil mønstre fordi den ikke kjenner hele kodebasen din, og rett og slett overkomplisering — kode og abstraksjoner du aldri ba om. Konklusjonen er ikke å slutte med AI, men å verifisere systematisk.

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

Lag på lag av forsvar — menneskelig vurdering legger fundamentet, automatiske tester bygger oppå.

Note: Tenk på verifisering som en pyramide. Nederst ligger det brede, billige fundamentet — menneskelig plan- og kodegjennomgang, som fanger de dyreste feilene før koden i det hele tatt skrives. Oppå det bygger de automatiske lagene: statisk analyse, enhetstester, integrasjonstester og E2E. Jo høyere opp, jo nærmere ekte bruk kommer vi — men også tregere og dyrere. Poenget er at ingen enkelt lag holder alene; det er lagene til sammen som gir trygghet. Nå går vi gjennom dem ett for ett, nedenfra og opp.

---

<span class="kicker">Del 1 · Lag 1/5 · Fundamentet</span>

## Kode- & plangjennomgang

<p class="lead">Viktig steg ved bruk av AI – med ekstra fokus på plangjennomgang.</p>

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

Note: Lag én, fundamentet, er menneskelig gjennomgang av både plan og kode. Dette laget fanger de dyreste feilene — feil arkitektur eller feil tilnærming — som ingen test ville oppdaget, fordi koden teknisk sett kan være helt feilfri og likevel løse feil problem. Og det er nettopp her det er billigst å rette: før en eneste linje er skrevet.

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

Note: Lag to er statisk analyse — kompilatoren og linteren, altså TypeScript og lint. Det fanger syntaks-, type- og skrivefeil før koden i det hele tatt kjøres — som «user.nmae» i stedet for «user.name». Det går på millisekunder, er helautomatisk og alltid på.

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

Note: Lag tre er enhetstester, som sjekker logikken i enkeltfunksjoner isolert — for eksempel en skatteberegning som gir feil sum. Når en enhetstest feiler, vet du nesten nøyaktig hvor problemet ligger. De er raske og presise, og utgjør ryggraden i en god testsuite.

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

Note: Lag fire er integrasjonstester, som fanger feilene i samspillet mellom komponenter — der hver del fungerer fint alene, men ikke sammen. Det klassiske eksempelet er at API-et leverer helt riktig data, men frontend viser den ikke. Hver del kan altså være korrekt, og likevel knirker koblingen.

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

Note: Øverst, lag fem, ligger E2E-testene. De følger hele brukerflyten slik en ekte bruker opplever den — for eksempel om brukeren faktisk får fullført en checkout. De gir bredest dekning, men er tregest og sier minst om akkurat hvor feilen ligger. Derfor toppen av pyramiden: verdifullt, men ikke noe du baserer alt på.

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

- Mer (AI-skrevet) kode krever mer og bedre verifisering — manuell review skalerer ikke
- **Fail fast, fail loud:** kjør de billigste sjekkene først
- Feil oppdaget tidlig = rask, billig tilbakemelding

Note: Så til hvordan vi binder lagene sammen. Manuell gjennomgang skalerer ikke når kodemengden femdobles — men pipelines gjør det. Nøkkelprinsippet er «fail fast»: kjør de raskeste og billigste sjekkene først, slik at en typefeil stopper deg etter to sekunder i stedet for fem minutter. Jo tidligere feilen oppdages, jo raskere og billigere er tilbakemeldingen.

---

<span class="kicker">Del 1 · Pre-commit hooks</span>

## Pre-commit hooks

- Kjør **typecheck + lint før** commit — ikke etter push
- Fang trivielle feil lokalt, på sekunder
- Enda kortere feedback-løkke enn CI/CD alene
- CI/CD blir sikkerhetsnettet, ikke førstelinjen
- Gjelder også **AI-en:** kjører den `git commit`, må den gjennom de samme sjekkene

<div class="bv-corner bv-br"><svg class="bv-fig"><use href="#bv-test"/></svg></div>

Note: Pre-commit-hooks flytter de raskeste sjekkene helt frem til commit-øyeblikket — typecheck og lint før commit, ikke etter push. Du fanger de trivielle feilene lokalt, på sekunder, før de i det hele tatt når repoet. Det gir en enda kortere feedback-løkke enn CI/CD alene, og lar CI/CD være sikkerhetsnettet i stedet for førstelinjeforsvaret. Og dette gjelder ikke bare mennesket: når AI-agenten selv kjører `git commit`, treffer den nøyaktig de samme hookene — den slipper ikke unna verifiseringen, og kan ikke committe kode som ikke passerer typecheck og lint.

---

<span class="kicker">Del 1 · Pre-commit hooks</span>

## Slik ser det ut

<style>
.reveal pre { background: var(--c-white); padding: 0.8em 1em; }
.reveal pre code, .reveal pre code * { color: var(--c-ink) !important; background: transparent !important; }
</style>

```json
// package.json
{
  "husky": {
    "hooks": {
      "pre-commit": "pnpm typecheck && pnpm lint:staged"
    }
  }
}
```

<p class="lead">Typecheck og lint kjører automatisk — hver eneste commit.</p>

Note: Slik ser det konkret ut med Husky — hele oppsettet ligger i package.json. Før hver commit kjøres typecheck og lint på de stagede filene, og commit-en stoppes hvis noe feiler. Poenget er at ingen lenger er avhengig av å huske å kjøre sjekkene — de er bakt inn i arbeidsflyten.

---

<span class="kicker">Del 1 · Pre-push hooks</span>

## Pre-push: hele testsuiten

```json
// package.json
{
  "husky": {
    "hooks": {
      "pre-commit": "pnpm typecheck && pnpm lint:staged",
      "pre-push": "pnpm typecheck && pnpm test"
    }
  }
}
```

<p class="lead">De tyngre sjekkene kjører før koden forlater maskinen.</p>

Note: Pre-push-hooken er det siste lokale forsvaret før koden går til remote. Her har vi råd til de tyngre sjekkene: full typecheck og hele testsuiten med «pnpm test». Mislykkes noe, stoppes pushen. Arbeidsdelingen er hele poenget — raske sjekker på hver commit, den tunge suiten på push — så du verken venter unødig ofte eller pusher noe ødelagt.

---

<span class="kicker">Del 1 · Hele flyten</span>

## Slik henger det sammen

<style>
.reveal .flowmap { display: flex; align-items: stretch; gap: 0.55em; margin: 1.1em -3% 0.6em; }
.reveal .flowmap .phase {
  display: flex; flex-direction: column;
  border: 2px dashed var(--c-line); border-radius: 18px;
  background: var(--c-cream); padding: 0.55em 0.8em 0.85em;
}
.reveal .flowmap .phase-label {
  text-align: center; font-size: 0.42em; font-weight: 700;
  text-transform: uppercase; letter-spacing: 0.1em;
  color: var(--c-skyink); margin-bottom: 0.45em;
}
.reveal .flowmap .phase .flow { margin: auto 0; }
.reveal .flowmap .flow .step {
  font-size: 0.46em; padding: 0.6em 0.45em; line-height: 1.25;
  overflow-wrap: normal; hyphens: manual;
}
.reveal .flowmap .flow .step + .step { margin-left: 1.5em; }
.reveal .flowmap .flow .step + .step::before { left: -0.82em; font-size: 1.45em; font-weight: 800; color: var(--c-skyink); }
.reveal .flowmap .step.rpi-anchor { position: relative; }
.reveal .flowmap .ai-note {
  position: absolute; top: calc(100% + 1.1em); left: 50%; transform: translateX(-50%);
  display: flex; flex-direction: column; align-items: center; line-height: 1.1;
  color: var(--c-skyink); font-weight: 800; white-space: nowrap;
}
.reveal .flowmap .ai-note .up { font-size: 2.4em; line-height: 0.7; }
.reveal .flowmap .ai-note .lbl { font-size: 1.35em; letter-spacing: 0.02em; }
.reveal .flowmap .bigarrow {
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  color: var(--c-skyink); font-weight: 800; line-height: 1;
}
.reveal .flowmap .bigarrow .ar { font-size: 2em; }
.reveal .flowmap .bigarrow .lbl {
  font-size: 0.36em; font-weight: 700; text-transform: uppercase;
  letter-spacing: 0.06em; margin-top: 0.3em;
}
</style>

<div class="flowmap">
<div class="phase" style="flex:3">
<span class="phase-label">Under utvikling</span>
<div class="flow">
<div class="step rpi-anchor">Implemen&shy;tasjon<span class="ai-note"><span class="up">↑</span><span class="lbl">RPI + AI</span></span></div>
<div class="step">pre-commit<br><strong>typecheck + lint</strong></div>
<div class="step">pre-push<br><strong>hele testsuiten</strong></div>
</div>
</div>
<div class="bigarrow"><span class="ar">→</span><span class="lbl">git push</span></div>
<div class="phase" style="flex:5">
<span class="phase-label">CI/CD</span>
<div class="flow">
<div class="step">TypeScript</div>
<div class="step">Lint</div>
<div class="step">Enhets&shy;tester</div>
<div class="step">Integra&shy;sjon</div>
<div class="step">E2E</div>
</div>
</div>
</div>

Note: La oss zoome ut og se hele flyten under ett. Den deler seg foreløpig i to bolker. Først «under utvikling»: alt som skjer lokalt på maskinen din mens koden blir til. Her er pre-commit og pre-push den løpende verifiseringen etter hver implementasjon — de raske sjekkene på commit, den tunge testsuiten på push. Når koden så forlater maskinen, tar CI/CD over som én samlet bolk — hele pipelinen fra typecheck til E2E, sikkerhetsnettet som fanger det som måtte slippe gjennom lokalt. Poenget er at verifiseringen er kontinuerlig og lagdelt gjennom hele løpet, ikke en engangssjekk på slutten.

---

<span class="kicker">Del 1 · TDD med AI</span>

## Test-drevet AI-utvikling

<div class="flow">
<div class="step"><strong>DU</strong><br>skriver tester<br>(feiler)</div>
<div class="step"><strong>AI</strong><br>skriver kode<br>(passerer)</div>
<div class="step"><strong>DU</strong><br>verifiserer &amp;<br>refaktorerer</div>
</div>

- Testene er **konkrete mål** AI-en skal treffe — verifiser, ikke håp
- Testene er **entydig kommunikasjon** — bedre enn «håndter edge cases» i fritekst

Note: TDD snur arbeidsflyten på hodet: du skriver testen som feiler først, AI skriver koden som får den til å passere, og så verifiserer og refaktorerer du. Testen blir både et konkret, målbart mål AI-en skal treffe, og en helt entydig spesifikasjon. Det er mye mer presist enn å be AI om å «håndtere edge cases» i fritekst.

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

Note: Tradisjonell kodegjennomgang betyr å lese hundrevis av linjer, ofte når det allerede er for sent å snu retning. Med RPI gjennomgår du i stedet en kort plan på rundt femti linjer. Da fanger du de dyre feilene — feil arkitektur eller feil tilnærming — på minutter, før en eneste linje kode er skrevet. La heller CI/CD ta detaljene.

---

<span class="kicker">Del 1 · RPI, oppdatert</span>

## Oppdatert RPI: Planen alene er ikke nok

<div class="contrast">
<div class="panel from">

#### Opprinnelig RPI

«Gjennomgå planen, ikke koden.» 50 linjer plan slår 500 linjer kode.

</div>
<div class="arrow">→</div>
<div class="panel to">

#### Nyere RPI (2026)

En overbevisende plan kan skjule feil tekniske antakelser. Kodegjennomgang er **obligatorisk igjen** — men lettere, fordi mer avklares før koden skrives.

</div>
</div>

<p style="font-size:0.82em">Avklaringen flyttes tidligere og deles opp: <strong>Spørsmål → Research → Design → Struktur → Plan</strong> — da blir kodegjennomgangen rask, ikke overflødig.</p>

<blockquote style="font-size:0.74em; margin:0.9rem 0 0">«Plans that read well don't necessarily build well.»<br><span style="opacity:.75">— Dexter Horthy, «Everything We Got Wrong» (2026)</span></blockquote>

Note: Dette er en viktig oppdatering fra mannen bak RPI, Dexter Horthy i HumanLayer. Opprinnelig var rådet å lese planen i stedet for koden — en kort plan er lettere å vurdere enn tusenvis av linjer. Men etter et år i produksjon innrømte han i foredraget «Everything We Got Wrong» at det var for enkelt: en plan kan lese godt og likevel bygge dårlig, fordi den skjuler feil tekniske antakelser — og teamet måtte rive ut og bygge om store deler av systemet. Løsningen var ikke å droppe plangjennomgang, men å flytte avklaringen enda tidligere og dele den opp i flere små steg, og samtidig gjøre kodegjennomgang obligatorisk igjen — bare lettere, fordi det meste allerede er avklart.

---

<span class="kicker">Del 1 · Hele flyten</span>

## Review lukker sløyfa

<style>
/* scoped to this slide so the other flow slide is untouched */
.reveal .rev2 .flowmap { margin: 1.1em -12% 0.7em; }
.reveal .rev2 .flowmap .phase { padding: 0.65em 0.9em 1em; }
.reveal .rev2 .flowmap .flow .step { padding: 0.95em 0.7em; line-height: 1.35; font-size: 0.42em; }
.reveal .rev2 .flowmap .flow .step + .step { margin-left: 1.3em; }
.reveal .rev2 .flowmap .flow .step + .step::before { left: -0.72em; }
.reveal .rev2 .flowmap .flow .step.review { background: #e7f4ee; }

/* RPI + AI: light labelled group around plan-review + implementasjon */
.reveal .rev2 .flowmap .flow .rpigroup {
  flex: 2.1; display: flex; flex-direction: column;
  border: 1.5px solid var(--c-skyink); border-radius: 14px;
  background: rgba(201,111,46,0.05); padding: 0.4em 0.55em 0.55em;
}
.reveal .rev2 .flowmap .flow .rpigroup .rpilabel {
  text-align: center; font-size: 0.38em; font-weight: 800; color: var(--c-skyink);
  text-transform: uppercase; letter-spacing: 0.08em; margin-bottom: 0.45em;
}
.reveal .rev2 .flowmap .flow .rpigroup .rpiinner { display: flex; flex: 1; }
.reveal .rev2 .flowmap .flow .rpigroup .rpiinner .step + .step { margin-left: 1.1em; }
.reveal .rev2 .flowmap .flow .rpigroup .rpiinner .step + .step::before { left: -0.62em; font-size: 1.2em; }
.reveal .rev2 .flowmap .flow .rpigroup + .step { margin-left: 1.3em; position: relative; }
.reveal .rev2 .flowmap .flow .rpigroup + .step::before {
  content: '→'; position: absolute; left: -0.72em; top: 50%; transform: translateY(-50%);
  color: var(--c-skyink); font-weight: 800; font-size: 1.45em;
}

/* slim down-arrow + review row right under CI/CD */
.reveal .rev2 .downconn { display: flex; justify-content: flex-end; margin: 0.55em -12% 0; }
.reveal .rev2 .downconn .col { flex: 0 0 58%; display: flex; align-items: center; justify-content: center; }
.reveal .rev2 .downconn .ar { font-size: 1.8em; font-weight: 400; color: var(--c-skyink); line-height: 0.6; }
.reveal .rev2 .flowmap.review-line { justify-content: flex-end; margin: 0.55em -12% 0; }
.reveal .rev2 .flowmap.review-line .phase { flex: 0 0 58%; }
</style>

<div class="rev2">

<div class="flowmap">
<div class="phase" style="flex:4.6">
<span class="phase-label">Under utvikling</span>
<div class="flow">
<div class="rpigroup">
<span class="rpilabel">RPI + AI</span>
<div class="rpiinner">
<div class="step review">Plan-review</div>
<div class="step">Implemen&shy;tasjon</div>
</div>
</div>
<div class="step">pre-commit<br><strong>typecheck</strong></div>
<div class="step">pre-push<br><strong>testsuite</strong></div>
</div>
</div>
<div class="bigarrow"><span class="ar">→</span><span class="lbl">git push</span></div>
<div class="phase" style="flex:5">
<span class="phase-label">CI/CD</span>
<div class="flow">
<div class="step">TypeScript</div>
<div class="step">Lint</div>
<div class="step">Enhets&shy;tester</div>
<div class="step">Integra&shy;sjon</div>
<div class="step">E2E</div>
</div>
</div>
</div>

<div class="downconn"><div class="col"><span class="ar">↓</span></div></div>

<div class="flowmap review-line">
<div class="phase">
<span class="phase-label">Review · etter CI/CD</span>
<div class="flow">
<div class="step review">AI kode- &amp; feature-review</div>
<div class="step review">Human review</div>
</div>
</div>
</div>

</div>

Note: Dette er det fulle bildet, med review-sløyfa lagt på. Legg merke til at review skjer i begge ender: helt til venstre, før en eneste linje kode skrives, gjør vi en plan-review — det er den oppdaterte RPI-tankegangen, å avklare og gjennomgå planen tidlig. Så går koden gjennom den lokale verifiseringen og CI/CD som før. Til slutt, etter at pipelinen er grønn, lukkes sløyfa med en egen review-fase: først en AI-drevet kode- og feature-gjennomgang, så en menneskelig review. Poenget er at review ikke er ett enkelt steg på slutten, men rammer inn hele løpet — planen vurderes før, koden vurderes etter.

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

Note: Denne kontrasten er kjernen i hele del 1. Blind tillit — «AI-en vet best» — fører til en nedadgående spiral av bugs, sikkerhetshull og teknisk gjeld, og dermed mistillit over tid. Verifisert tillit — «AI-en har bevist det» — vokser i stedet, fordi den bygger på bevis: grønne tester, grønn CI/CD, godkjent plan. Utviklerens nye jobb er å definere suksess, gjennomgå planer, bygge pipelines og verifisere — ikke å skrive hver linje selv.

---

<span class="kicker">Del 1 · Oppsummering</span>

## Nøkkelpunkter — Del 1

- **Tillitsunderskuddet:** mange stoler ikke på AI — og det er rasjonelt
- **Verifiseringspyramiden:** lag på lag av forsvar
- **CI/CD er kritisk:** automatiser og fail fast
- **TDD med AI:** du skriver testene, AI implementerer
- **Plangjennomgang:** 50 linjer plan > 500 linjer kode

Note: La oss oppsummere del 1. Tillitsunderskuddet er rasjonelt, og svaret er lagdelt verifisering. Vi automatiserer med CI/CD og «fail fast», vi snur arbeidsflyten med TDD der du eier testene og AI implementerer, og vi flytter gjennomgangen fra kode til plan. Dette er fundamentet vi nå bygger den praktiske delen på.

---

<!-- .slide: class="section-header" data-background-gradient="linear-gradient(150deg, #eaf0f4 0%, #f0e4cc 100%)" -->

## Del 2 · Beste praksis og praktisk anvendelse

<div class="bv-scene bv-center"><svg class="bv-fig" style="width:160px"><use href="#bv-mountain"/></svg><svg class="bv-fig" style="width:120px"><use href="#bv-hills"/></svg></div>

Note: Nå som vi vet hvordan vi verifiserer, løfter vi blikket til de overordnede prinsippene — og hvordan du faktisk kommer i gang i praksis.

---

<span class="kicker">Del 2 · Fra teori til praksis</span>

## Fra teori til praksis

<p class="lead">Ikke en ferdig fasit — «beste praksis» endrer seg ekstremt fort.</p>

- Kjenn fundamentet — så kan teamet velge hvordan dere tilpasser AI best
- Kjenner du «beste praksis», er det lettere å henge med videre

<div class="bv-corner bv-br"><svg class="bv-fig"><use href="#bv-mountain"/></svg></div>

Note: En viktig ramme før vi dykker ned: beste praksis for AI-utvikling er et bevegelig mål. Det som gjelder i dag, kan være forandret om noen måneder, så dette er ingen fasit. Men kjenner du fundamentet, kan teamet ditt selv vurdere hvordan dere bør tilpasse AI-bruken til akkurat dere — og kjenner du gårsdagens beste praksis, er det mye lettere å henge med videre. Vi starter med ett av fundamentene: compounding engineering.

---

<span class="kicker">Del 2 · Compounding engineering</span>

## Compounding engineering

<p class="lead">Investeringer i utviklingsprosessen som gir utbytte over tid.</p>

- Ikke engangsforbedringer — **systemer som blir bedre jo mer du bruker dem**
- Analogi: rentes rente, men for utviklingspraksis
- Hver forbedring gjør neste AI-interaksjon bedre

<div class="bv-corner bv-br"><svg class="bv-fig"><use href="#bv-shapes"/></svg></div>

Note: Compounding engineering handler om at investeringer i selve prosessen forrenter seg. En god testsuite gjør AI-koden bedre, det gjør utviklingen raskere, og det frigjør tid til å forbedre testsuiten enda mer. Det er rentes rente, bare for utviklingspraksis — en positiv spiral der hver forbedring gjør neste AI-interaksjon bedre.

---

<span class="kicker">Del 2 · Compounding i praksis</span>

## Compounding i praksis

<div class="cards">
<div class="card">

#### Domeneminne

Skriv `auth.md` én gang → spar timevis med gjentatt forklaring senere.

</div>
<div class="card">

#### Test suite

En investering som fanger stadig flere bugs over tid — og et tankeskifte fra «fikset buggen» til «la til en test som forhindrer denne typen bug».

</div>
<div class="card">

#### Delt domenespråk

En levende ordliste over domenebegrepene holder AI-ens språk i tråd med vårt — skrevet én gang, brukt overalt.

</div>
</div>

<p class="lead">En god kodebase blir enda viktigere med AI — den hermer ukritisk etter eksemplene den finner.</p>

Note: Konkret ser det slik ut. Domeneminne du skriver én gang — for eksempel en auth.md — sparer deg titalls timer med gjentatt forklaring senere. Test-tankesettet er to ting i ett: testsuiten fanger stadig mer over tid, og det viktigste er tankeskiftet fra «jeg fikset buggen» til «jeg la til en test som forhindrer hele denne typen bug». Her er det verdt å understreke at en god kodebase alltid teller, men teller enda mer med AI — den baserer seg relativt ukritisk på de eksemplene den finner, gode som dårlige, så kvaliteten på det som allerede ligger der forplanter seg videre. Og en delt domeneordliste holder AI-ens begreper i tråd med vårt eget språk.

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

<p><em>Mer er ikke alltid bedre — forbedre det du allerede har.</em></p>

<div class="bv-corner bv-tr bv-sm"><svg class="bv-fig"><use href="#bv-tree"/></svg></div>

Note: Og her er compounding satt i system, som en enkel løkke: du gjør en oppgave med AI, legger merke til friksjonen — måtte du forklare det samme flere ganger? — og så dokumenterer du løsningen som en rule, en skill eller en test. Neste oppgave blir litt lettere, og du gjentar. Dette er compounding engineering konkretisert. Og husk: mer er ikke alltid bedre — det handler vel så mye om å skjerpe og forbedre det du allerede har som å legge til nytt. Dette er broen videre til de ti bud.

---

<span class="kicker">Del 2 · De ti bud (1–5)</span>

## De ti bud

1. **Ikke outsource tenkingen** — AI forsterker, erstatter ikke
2. **Hold konteksten ren** — under 40 %, komprimer, start friskt
3. **Definer suksess før implementering** — tester & akseptansekriterier
4. **Aldri ship uverifisert kode** — AI-kode trenger *mer* verifisering
5. **Gjennomgå planer**, ikke bare kode

Note: De fem første budene handler om disiplin og kvalitetssikring. Ikke outsource selve tenkingen — AI forsterker, den erstatter ikke. Hold konteksten ren, under førti prosent. Definer hva suksess betyr før implementering, med tester og akseptansekriterier. Send aldri uverifisert kode — AI-kode trenger mer verifisering, ikke mindre. Og gjennomgå planer, ikke bare kode.

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

Note: De fem siste handler om systemene rundt arbeidet. Bygg domeneminne med CLAUDE.md, rules og ordlister. Følg RPI konsekvent. Ikke vær redd for å starte friske sesjoner — det er god hygiene, ikke en fiasko. Invester i compounding ved å dokumentere mønstre og bygge systemer. Og behold den pragmatiske skepsisen: «trust, but verify».

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

Note: Dette er erfaringer fra egne prosjekter, ikke en fasit — men noen mønstre har gått igjen. Lav WIP, altså én til to oppgaver om gangen, ser ut til å holde kvaliteten oppe. Det å dele samme AGENTS.md og skills på tvers av Claude, Cursor, Codex og Copilot sparer mye vedlikehold, fordi reglene bor ett sted. Eksplisitte «Never Break»-regler blir stort sett respektert. Og en dokumentert prosess via skills har gitt jevnere kvalitet.

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

Note: To ting vi ikke så komme i starten. For det første: artefaktene — rules, skills og planer — blir mye mer verdt når de ligger i git og deles, enn når de bor lokalt hos én person. Da eier teamet dem sammen, de kan reviewes, og forbedringer kommer alle til gode. For det andre: den samme dokumentasjonen som gjør AI bedre, korter også ned onboarding for nye folk. Vår erfaring er rett og slett at jo mer vi la i felles filer, jo mindre måtte vi forklare på nytt.

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

Note: Tre konkrete lærdommer. Den første: la AI kjøre repo-scriptene — pnpm check og pnpm test — i stedet for de rå verktøyene som tsc eller eslint direkte. Skriptet kapsler inn riktige flagg og stier, så hver kjøring blir lik. Den andre: legg inn et fast rydde-pass når koden virker — forenkle først, så luk bort typisk AI-støy som døde sjekker og støyende kommentarer. Og den tredje, motsatt vei: ikke dokumentér alt i .md-filer — det blir mye å vedlikeholde, og en glemt oppdatering gjør fort at dokumentasjonen lyver.

---

<span class="kicker">Del 2 · Automatiske vakter</span>

## Et knippe automatiske vakter

| Sjekk | Hva det fanger | Kommando |
|---|---|---|
| Typer | type- og skrivefeil før kjøring | `npm run typecheck` |
| Lint | regelbrudd og risikomønstre | `npm run lint` |
| **jscpd** | kopiert/limt kode på tvers av filer | `npx jscpd .` |
| **knip** | ubrukte filer, eksporter og avhengigheter | `npx knip` |
| **osv-scanner** | kjente sårbarheter (CVE) i avhengigheter | `npx osv-scanner` |

Alt samlet bak ett repo-script: `npm run check`.

Note: Statisk analyse er mer enn bare en linter. jscpd er en copy-paste-detektor — den finner kode som er duplisert på tvers av filer, så samme logikk ikke lever fem steder. knip finner død kode: filer, eksporter og pakker ingen bruker lenger. Og osv-scanner, fra Google, sjekker avhengighetene mot databasen over kjente sårbarheter. Ingen av dem trenger å starte appen, og alt gjemmes bak ett repo-script — npm run check — så det alltid kjøres likt, av både mennesker og AI.

---

<span class="kicker">Del 2 · Token-økonomi</span>

## Optimaliser token-bruk

<div class="cards two">
<div class="card">

#### Enkelt

- Hold konteksten **ren**
- Bruk billigere modeller til enklere oppgaver — f.eks. planlegging med GPT-5.5, implementasjon med GPT-5.4 (eller billigere)
- Vurder hvor mye **thinking/reasoning effort** modellen faktisk trenger

</div>
<div class="card">

#### Avansert

- Verktøy som presenterer konteksten til AI mer effektivt
- Antall **skills** o.l. øker konteksten hver samtale starter med
- Lange filer koster — AI søker etter relevante filer og leser kanskje hele fila

</div>
</div>

Note: Token-bruk handler om både økonomi og kvalitet — en ren, fokusert kontekst gir både bedre svar og lavere kostnad. Det enkle først: rydd i konteksten, bruk en billigere modell til de enklere oppgavene, og skru ned «thinking»-nivået når oppgaven ikke krever dyp resonnering. Det mer avanserte handler om hva som fyller konteksten i utgangspunktet — verktøy som leverer kontekst smartere, hvor mange skills du har lastet, og hvor lange filene i prosjektet er, siden AI gjerne leser hele filer når den leter etter relevant kode.

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

Note: De fleste problemer har et kjent motgift, og denne tabellen er nesten en feilsøkingsguide. Lange sesjoner løser du med progress-filer og førti-prosent-regelen. Blind tillit med CI/CD, TDD og code review. Monolittiske oppgaver ved å bryte dem ned i atomiske biter. Kjenner du symptomet, kjenner du som regel løsningen.

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

Note: Modningskurven er bevisst overkommelig, så ingen skal føle at dette er alt-eller-ingenting. Dag én lager du en CLAUDE.md med stack, kritiske regler og kommandoer. I løpet av uka din første rules-fil. I løpet av måneden en delt domeneordliste. Og i løpet av kvartalet dokumenterer du en arbeidsflyt som en skill. Du trenger altså ikke alt fra dag én — det bygges opp gradvis.

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

Note: Dette er hele reisen samlet på ett bilde. Fra vibe coding til strukturert RPI, fra blind til verifisert tillit, fra kaotisk kontekst til domeneminne, fra manuell review til CI/CD og plangjennomgang, og fra engangsløsninger til compounding. Poenget er at det ikke er seks separate endringer, men én sammenhengende modning.

---

<!-- .slide: class="section-header" data-background-gradient="linear-gradient(150deg, #eaf0f4 0%, #f0e4cc 100%)" -->

## Takk for oss! Spørsmål?

<p class="lead">Verifiser og standardiser — invester i prosessen.</p>

<div class="bv-scene bv-center"><svg class="bv-fig" style="width:170px"><use href="#bv-mountain"/></svg><svg class="bv-fig" style="width:130px"><use href="#bv-hills"/></svg></div>

Note: Helt kort oppsummert: verifiser og standardiser arbeidet, og invester i selve prosessen, så den forrenter seg over tid. Det er det som skiller ekte akselerasjon fra teknisk gjeld. Tusen takk for oppmerksomheten — så åpner jeg for spørsmål.
