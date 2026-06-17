# Generieke vCISO — Sub-project 1: Onderzoek + Blueprint — Implementatieplan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.
>
> **Let op — dit is een onderzoeks-/synthese-deliverable, geen software.** TDD (failing test → code → pass) is niet van toepassing. In plaats daarvan geldt per taak een **verificatie-gate**: de vooraf vastgelegde scorekaart (Taak 0) is de "test", en elke bevinding moet die invullen (alle velden + bron-citaat) voordat een taak "slaagt".
>
> **ATLAS routing-gate:** elke schrijfactie naar een bestand vereist eerst een routing-blok (domein · bestemming · aard · muur-check · reden) en akkoord van Bas. De stappen hieronder benoemen dat expliciet waar geschreven wordt.

**Goal:** Een diep & breed, bronvermeld open-source-onderzoek opleveren dat resulteert in één generieke vCISO-blueprint: OSS-landschap per NIST CSF 2.0-functie, capability-map, gap-analyse en orkestratie-ontwerp.

**Architecture:** Per CSF-functie (Govern · Identify · Protect · Detect · Respond · Recover) één deep-research-sweep (multi-source, fact-checked, geciteerd) → losse findings-bestanden → synthese tot één blueprint. Een vooraf vastgelegde scorekaart standaardiseert elke tool-beoordeling. Mens-in-de-loop review vóór de blueprint definitief is.

**Tech Stack:** `deep-research`-skill (web-onderzoek-harness), Markdown-deliverables in de cisochat git-repo. Geen code, geen build.

**Scope-grens (YAGNI):** dit plan stopt bij de goedgekeurde blueprint + roadmap. Het bóuwen van capabilities is sub-project 2 e.v. (eigen brainstorm → spec → plan). Geen organisatie-specifieke (bv. gemeentelijke) inhoud — die laag komt later en apart.

---

## Bestandsstructuur

| Bestand | Verantwoordelijkheid |
|---|---|
| `docs/vciso/00-scorekaart.md` | Beoordelingscriteria + onderzoeksprotocol — de "test" waar elke bevinding aan moet voldoen |
| `docs/vciso/research/govern.md` | Deep-research findings CSF-functie Govern (geciteerd) |
| `docs/vciso/research/identify.md` | idem Identify |
| `docs/vciso/research/protect.md` | idem Protect |
| `docs/vciso/research/detect.md` | idem Detect |
| `docs/vciso/research/respond.md` | idem Respond |
| `docs/vciso/research/recover.md` | idem Recover |
| `docs/vciso/research/ai-vciso-meta.md` | Cross-cutting findings: bestaande AI-vCISO/"CISO-in-a-box"-projecten (Taak 6b) |
| `docs/vciso/vciso-blueprint.md` | **De deliverable:** OSS-landschap + capability-map + gap-analyse + orkestratie-ontwerp |
| `docs/vciso-blueprint-ontwerp.md` | (bestaat al) ontwerp-spec — leesreferentie, niet wijzigen |

Findings-bestanden zijn onderling onafhankelijk (parallelliseerbaar). De blueprint synthetiseert ze.

---

## Taak 0: Scorekaart + onderzoeksprotocol vastleggen

**Files:**
- Create: `docs/vciso/00-scorekaart.md`

- [ ] **Stap 1: Routing-blok tonen en akkoord afwachten**

Toon Bas:
> 📍 Routing-voorstel — Domein: commons · Bestemming: `docs/vciso/00-scorekaart.md` · Aard: NIEUW · Muur-check: ✅ generiek/open source · Reden: standaardiseert de tool-beoordeling vóór het onderzoek.

Wacht op akkoord. Geen akkoord = niet schrijven.

- [ ] **Stap 2: Scorekaart schrijven**

Schrijf `docs/vciso/00-scorekaart.md` met exact deze inhoud:

```markdown
# vCISO OSS-scorekaart & onderzoeksprotocol

> Standaardiseert elke open-source-toolbeoordeling in het vCISO-onderzoek. Elke tool in de
> research/-bestanden MOET alle velden ingevuld hebben, met minstens één bron-citaat per claim.

## Beoordelingsvelden (per tool)

| Veld | Toelichting | Schaal/format |
|---|---|---|
| Naam + URL | Projectnaam en canonieke repo/site | tekst + link |
| CSF-functie(s) | Welke van Govern/Identify/Protect/Detect/Respond/Recover | enum |
| Capability | Welke vCISO-capability het invult | tekst |
| Korte omschrijving | Wat het doet, in 1–2 zinnen | tekst |
| Rijpheid | Onderhoud: laatste release, commit-activiteit, contributors | hoog / midden / laag + onderbouwing |
| Licentie | SPDX-identifier + copyleft-implicatie voor open-core | tekst |
| EU-soevereiniteit | Zelf-hostbaar? Data buiten EU nodig? (zachte weging, zie rubriek) | ja/nee + toelichting |
| Integreerbaarheid | API / MCP / CLI / library; koppelbaar aan een dirigent? | enum + toelichting |
| AI-native koppelbaarheid | LLM-/agent-vriendelijk? MCP-server, schone API, gestructureerde output? | ja/deels/nee + toelichting |
| Stack/taal | Implementatietaal en runtime-eisen | tekst |
| Fit-score | Geschiktheid als vCISO-orgaan | 1–5 + 1 zin motivatie |
| Bronnen | Citaten die de bovenstaande claims dekken | links |

## Harde poort — open source only
Alleen écht open-source software komt in de findings. **Geen commerciële/proprietary tools.** Bij
**open-core** projecten (gratis community-editie + betaalde editie): beoordeel uitsluitend de
open-source community-editie, en noteer expliciet welke vCISO-relevante functies achter de betaalde
muur zitten. Puur-commerciële tools vallen volledig af (niet opnemen).

## Fit-score-rubriek (1–5)
- **5** — rijp, permissieve licentie, EU-soeverein/zelf-hostbaar, schone + AI-native integratie (MCP/API), actief onderhouden.
- **3** — bruikbaar maar met één serieus bezwaar (bv. copyleft dat open-core bemoeilijkt, zwakke/niet-AI-native API, of non-EU/SaaS-afhankelijkheid).
- **1** — bestaat, maar niet praktisch integreerbaar of niet onderhouden.
- **EU-weging (zacht):** non-EU of SaaS-only OSS mag opgenomen worden als het toonaangevend is, maar
  krijgt een expliciete waarschuwing en een lagere fit-score dan een vergelijkbaar EU-soeverein/zelf-hostbaar alternatief.

## Onderzoeksprotocol
1. Per CSF-functie een aparte deep-research-sweep (multi-source, fact-checked), plus één cross-cutting
   sweep naar bestaande AI-vCISO/"CISO-in-a-box"/GRC-copilot OSS-projecten (Taak 6b).
2. Breedte: elke sweep dekt zowel **governance/management**-tooling (GRC, ISMS, beleid, risk,
   rapportage) als **technische** tooling — niet alleen scanners.
3. Startbronnen: awesome-lists (bv. awesome-security, awesome-selfhosted), OWASP-projectenlijst,
   CNCF/Linux Foundation-landscapes, GitHub-topics, en onafhankelijke reviews — geen vendor-marketing
   als enige bron.
4. Elke tool-claim heeft minstens één onafhankelijk citaat. Onzekerheid expliciet benoemen.
5. Minimaal-volledigheid per functie: streef naar de relevante categorieën gedekt (niet één tool per
   functie). Bewust loggen wat NIET gevonden/gedekt is → voedt de gap-analyse.
6. Curatie: de sweeps zoeken breed (diep & breed), maar de blueprint (Taak 7) cureert per sub-categorie
   tot de top 2–3 volwaardige scorekaart-entries; de overige gevonden tools worden als "long tail" bij
   naam + URL genoemd, zonder volledige scorekaart.
7. Muur: geen proprietary/organisatie-specifieke bronnen of -IP in de open-source findings.
```

- [ ] **Stap 3: Verificatie-gate**

Controleer: alle 12 velden gedefinieerd, fit-rubriek aanwezig, harde open-source-poort + curatie-regel + citatie-eis benoemd in het protocol. Geen TODO's.

- [ ] **Stap 4: Commit**

```bash
cd /x/SECURITY-COMMONS-NL/cisochat
git add docs/vciso/00-scorekaart.md
git commit -m "docs(vciso): scorekaart + onderzoeksprotocol voor OSS-sweep"
```

---

## Taken 1–6: Deep-research-sweep per CSF-functie

> Deze zes taken zijn onderling onafhankelijk en mogen parallel (elk eigen findings-bestand). Elke taak volgt exact hetzelfde stappenpatroon; alleen de onderzoeksvraag en het doelbestand verschillen. De onderzoeksvraag per functie staat in de tabel onderaan deze sectie.

**Stappenpatroon (geldt voor elke taak 1–6):**

- [ ] **Stap A: Deep-research uitvoeren**

Roep de `deep-research`-skill aan met de functie-specifieke onderzoeksvraag (zie tabel). De vraag bevat altijd deze gemeenschappelijke kop:

> "Lever per tool de 12 scorekaart-velden (naam+URL · CSF-functie(s) · capability · korte omschrijving · rijpheid · licentie · EU-soevereiniteit · integreerbaarheid · AI-native koppelbaarheid · stack/taal · fit-score 1–5 · bronnen), met bron-citaten. **Harde poort: alleen écht open-source software — geen commerciële/proprietary tools; bij open-core beoordeel je alleen de gratis community-editie.** EU-soevereiniteit/zelf-hostbaarheid is een zachte weging: non-EU of SaaS-only OSS mag genoemd worden mét waarschuwing en lagere fit-score. Noteer per tool de **AI-native koppelbaarheid** (MCP-server, schone API, gestructureerde output) — relevant omdat de aansturende dirigent een AI is. Dek zowel governance/management-tooling als technische tooling. Benoem expliciet welke deel-capabilities GEEN volwassen OSS-optie hebben."

- [ ] **Stap B: Routing-blok tonen en akkoord afwachten**

> 📍 Routing-voorstel — Domein: commons · Bestemming: `docs/vciso/research/<functie>.md` · Aard: NIEUW · Muur-check: ✅ generiek/open source · Reden: findings-bestand CSF-functie <functie>.

- [ ] **Stap C: Findings wegschrijven**

Schrijf de deep-research-output naar `docs/vciso/research/<functie>.md`, geordend als één tool per sub-sectie met alle scorekaart-velden + een afsluitende "Niet-gedekt / gaps"-paragraaf.

- [ ] **Stap D: Verificatie-gate**

Controleer tegen de scorekaart: elke tool heeft alle 12 velden; elke claim heeft ≥1 citaat; de "Niet-gedekt"-paragraaf is ingevuld. Ontbreekt iets → terug naar Stap A voor die tool. Geen niet-geciteerde beweringen.

- [ ] **Stap E: Commit**

```bash
cd /x/SECURITY-COMMONS-NL/cisochat
git add docs/vciso/research/<functie>.md
git commit -m "docs(vciso): OSS-findings CSF-<functie>"
```

**Onderzoeksvragen per taak:**

| Taak | Functie | Doelbestand | Kern van de onderzoeksvraag (capabilities om te dekken) |
|---|---|---|---|
| 1 | Govern | `research/govern.md` | OSS voor securitystrategie/beleid, policy-as-code & policy-management, governance/rollen (RASCI), bestuurlijke rapportage/KPI-dashboards, ISMS/GRC-governance-modules |
| 2 | Identify | `research/identify.md` | OSS voor asset-/data-inventory (CMDB/discovery), risk register & risicobeoordeling, threat modeling, compliance-mapping & gap-analyse, threat-intel (bv. OpenCTI/MISP) |
| 3 | Protect | `research/protect.md` | OSS voor maatregelen-/control-management, security awareness & phishing-simulatie, IAM/access-governance, configuratie-baselines & hardening (bv. OpenSCAP, CIS-tooling), policy-as-code-enforcement |
| 4 | Detect | `research/detect.md` | OSS voor security posture / CSPM (bv. Prowler), vulnerability management (bv. OpenVAS/Greenbone), SIEM/monitoring (bv. Wazuh), detectie-engineering (Sigma/detection-as-code) |
| 5 | Respond | `research/respond.md` | OSS voor incident response / case management (bv. TheHive/Cortex), SOAR/playbook-automatisering, IR-runbooks, crisiscommunicatie-tooling |
| 6 | Recover | `research/recover.md` | OSS voor continuïteit/BCM (ISO 22301), backup/herstel-orchestratie, disaster-recovery-planning, lessons-learned/post-incident-review |

---

## Taak 6b: Cross-cutting sweep — bestaande AI-vCISO / "CISO-in-a-box" projecten

> Eén extra deep-research-sweep, dwars op de CSF-functies: bestaat er al open-source software die een CISO/vCISO probeert na te bootsen of te ondersteunen met AI? Voorkomt dat we het wiel heruitvinden en informeert het orkestratie-ontwerp (Taak 8).

**Files:**
- Create: `docs/vciso/research/ai-vciso-meta.md`

- [ ] **Stap A: Deep-research uitvoeren**

Roep de `deep-research`-skill aan met deze vraag (incl. de gemeenschappelijke kop uit Taken 1–6):
> "Welke **open-source** projecten bestaan die de rol van een (v)CISO geheel of deels nabootsen of ondersteunen met AI/LLM/agents? Denk aan: AI-GRC-copilots, security-/compliance-assistenten, agentische security-frameworks, policy-/risk-redeneer-agents, en orkestratielagen boven security-tools. Lever per project de scorekaart-velden plus: welke CSF-functies het raakt, welke aanpak (RAG / agents / workflow), en wat we ervan kunnen hergebruiken of lenen voor een dirigent-architectuur."

- [ ] **Stap B: Routing-blok tonen en akkoord afwachten**

> 📍 Routing-voorstel — Domein: commons · Bestemming: `docs/vciso/research/ai-vciso-meta.md` · Aard: NIEUW · Muur-check: ✅ generiek/open source · Reden: cross-cutting findings AI-vCISO-projecten.

- [ ] **Stap C: Findings wegschrijven**

Schrijf de output naar `docs/vciso/research/ai-vciso-meta.md`, één project per sub-sectie met scorekaart-velden + de extra velden (CSF-dekking, aanpak, herbruikbaarheid), en een afsluitende "Lessen voor de dirigent-architectuur"-paragraaf.

- [ ] **Stap D: Verificatie-gate**

Controleer tegen de scorekaart: harde poort (open source only) toegepast; elke claim geciteerd; de "Lessen"-paragraaf ingevuld.

- [ ] **Stap E: Commit**

```bash
cd /x/SECURITY-COMMONS-NL/cisochat
git add docs/vciso/research/ai-vciso-meta.md
git commit -m "docs(vciso): cross-cutting findings AI-vCISO/CISO-in-a-box projecten"
```

---

## Taak 7: Synthese — capability-map + gap-analyse

**Files:**
- Create: `docs/vciso/vciso-blueprint.md` (sectie 1–3)
- Read: alle `docs/vciso/research/*.md` (zes CSF-functies + `ai-vciso-meta.md`), `docs/vciso-blueprint-ontwerp.md`

- [ ] **Stap 1: Alle findings + spec inlezen**

Lees de zeven findings-bestanden (zes CSF-functies + de AI-vCISO-meta-sweep) en de ontwerp-spec (§3 capability-tabel, §4 organen-tabel) als invoer.

- [ ] **Stap 1b: Cross-functie-reconciliatie (dedup)**

Veel tools dekken meerdere CSF-functies (bv. Wazuh = Detect+Respond, OpenCTI = Identify+Detect, een GRC-suite = Govern+Identify+Protect) en zijn dan in meerdere findings-bestanden opgedoken. Maak één canonieke lijst: per tool één entry, met **alle** functies die het dient en **één** afgestemde fit-score. Los tegenstrijdige scores tussen sweeps op (kies de best onderbouwde, noteer waarom).

- [ ] **Stap 2: Routing-blok tonen en akkoord afwachten**

> 📍 Routing-voorstel — Domein: commons · Bestemming: `docs/vciso/vciso-blueprint.md` · Aard: NIEUW · Muur-check: ✅ generiek · Reden: synthese-deliverable van het onderzoek.

- [ ] **Stap 3: Blueprint secties 1–3 schrijven**

Schrijf `docs/vciso/vciso-blueprint.md` met:
- **§1 OSS-landschap** — samenvattende tabel: per CSF-functie de top-kandidaten (naam · fit-score · licentie · EU-soeverein · integratie · **AI-native**), plus per sub-categorie een **long-tail**-verwijzing (overige tools bij naam). Verwijs naar het bijbehorende findings-bestand.
- **§2 Capability-map** — tabel `CSF-functie → capability → kandidaat-invulling (bestaand Commons-tool / generieke AI-skill / externe OSS / **reasoning+RAG: geen tool** / nog-te-bouwen)`. Verrijk de §3/§4-tabellen uit de ontwerp-spec met de onderzoeksresultaten. **Markeer expliciet** de capabilities die geen tool kennen maar door de dirigent zelf (redeneren + RAG op normen) worden ingevuld — dat is het advies-brein van de vCISO en mag niet onder de gereedschapskist verdwijnen.
- **§3 Gap-analyse** — per CSF-functie wat ontbreekt of zwak is (verwacht zichtbaar: Respond, Recover), elk met de bron-paragraaf "Niet-gedekt" uit de findings.

- [ ] **Stap 4: Verificatie-gate (spec-dekking)**

Controleer: alle zes CSF-functies komen voor in §1, §2 én §3; cross-functie-dedup toegepast (geen tool dubbel met afwijkende scores); reasoning+RAG-capabilities expliciet gemarkeerd; curatie toegepast (top 2–3 + long tail per sub-categorie). Elke capability uit ontwerp-spec §3 staat in de capability-map. Geen lege cellen, geen "TBD".

- [ ] **Stap 5: Commit**

```bash
cd /x/SECURITY-COMMONS-NL/cisochat
git add docs/vciso/vciso-blueprint.md
git commit -m "docs(vciso): blueprint §1-3 — OSS-landschap, capability-map, gap-analyse"
```

---

## Taak 8: Orkestratie-ontwerp + roadmap

**Files:**
- Modify: `docs/vciso/vciso-blueprint.md` (sectie 4–5 toevoegen)

- [ ] **Stap 1: Routing-blok tonen en akkoord afwachten**

> 📍 Routing-voorstel — Domein: commons · Bestemming: `docs/vciso/vciso-blueprint.md` (aanvullen) · Aard: bestaand · Muur-check: ✅ · Reden: orkestratie-ontwerp + roadmap toevoegen.

- [ ] **Stap 2: §4 Orkestratie-ontwerp schrijven**

Voeg toe aan `docs/vciso/vciso-blueprint.md`:
- Hoe de dirigent (cisochat) een vraag routeert: CSF-functie-detectie → capability → instrumentkeuze.
- Beslissing router-mechanisme: prompt-routing vs. expliciete tool-aanroepen (MCP) — onderbouwd met de integreerbaarheid- en AI-native-bevindingen uit het onderzoek (welke tools bieden API/MCP) én de "Lessen voor de dirigent-architectuur" uit `ai-vciso-meta.md` (Taak 6b). Dit beantwoordt open punt §10 van de ontwerp-spec.
- Mens-in-de-loop- en audit-grenzen: welke stappen adviserend zijn vs. welke expliciete bevestiging vereisen; wat er gelogd wordt (audit-trail by design).

- [ ] **Stap 3: §5 Roadmap schrijven**

Voeg toe: gefaseerde bouwvolgorde voor sub-project 2 e.v., afgeleid van de gap-analyse, in CSF-volgorde van waarde (verwacht: Govern/Identify eerst — `grc-platform` staat al — daarna Detect, dan de gaps Respond/Recover). Per fase: doel, kandidaat-organen, en wat nog gebouwd moet worden.

- [ ] **Stap 4: Verificatie-gate**

Controleer: router-mechanisme is gekozen + onderbouwd met onderzoeksdata (niet aanname); mens-in-de-loop-grenzen expliciet; roadmap dekt alle zes functies en sluit aan op de gap-analyse (§3).

- [ ] **Stap 5: Commit**

```bash
cd /x/SECURITY-COMMONS-NL/cisochat
git add docs/vciso/vciso-blueprint.md
git commit -m "docs(vciso): blueprint §4-5 — orkestratie-ontwerp + roadmap"
```

---

## Taak 9: Mens-in-de-loop review-gate

- [ ] **Stap 1: Blueprint voorleggen aan Bas**

Vat samen: belangrijkste OSS-kandidaten per functie, de gaps, de router-keuze, en de voorgestelde bouwvolgorde. Vraag expliciet om akkoord of bijsturing. Beslis niets autonoom (Noorderster).

- [ ] **Stap 2: Verwerk feedback**

Bij wijzigingen: per schrijfactie opnieuw routing-blok → edit → verificatie-gate → commit. Herhaal tot Bas akkoord geeft.

- [ ] **Stap 3: Afronden**

Bij akkoord: noteer in de blueprint-status "vastgesteld" + datum. Sub-project 1 is klaar; sub-project 2 (eerste capability bouwen) start als eigen brainstorm-cyclus.

---

## Self-review (door de planner uitgevoerd)

**Spec-dekking:** ontwerp-spec §6 (onderzoek + blueprint-inhoud) → Taken 1–8. §3 capability-tabel → Taak 7 §2. §4 organen → Taak 7 §2. §10 open punten: deep-research-vraagstelling → Taak 0 + 1–6b; scorekaart → Taak 0; router-mechanisme → Taak 8 (mede gevoed door Taak 6b). §7 fasering → Taak 8 §5. §8 muren → routing-/muur-check in elke schrijfstap. Geen gaten.

**Placeholder-scan:** geen "TBD/TODO/later"; de scorekaart-inhoud staat volledig uitgeschreven in Taak 0; onderzoeksvragen staan concreet in de tabel bij Taken 1–6 en in Taak 6b.

**Type-/naamconsistentie:** bestandsnamen (`00-scorekaart.md`, `research/<functie>.md`, `research/ai-vciso-meta.md`, `vciso-blueprint.md`) consistent tussen bestandsstructuur, taken en commits; de **12** scorekaart-velden uit Taak 0 (incl. *AI-native koppelbaarheid*, harde open-source-poort) zijn exact wat de verificatie-gates van Taken 0 en 1–6b tellen; cross-functie-reconciliatie (Taak 7 stap 1b) en curatie-regel (protocol punt 6) zijn beide verankerd in de verificatie-gate van Taak 7 stap 4; de zeven sweeps (zes CSF-functies + AI-vCISO-meta) consistent door Taken 7–8.
