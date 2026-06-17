# cisochat als vCISO-dirigent — Ontwerp & Blueprint-opzet

> Ontwerp-spec. Verbreedt het oorspronkelijke [concept](concept.md) van cisochat (een RAG-chatbot
> met CISO-persona) naar een **generieke vCISO-orkestratielaag**: een AI-dirigent die de volle
> breedte van het CISO-werk nabootst door bestaande tools, skills en open-source software aan te
> sturen. Framework-agnostisch en generiek; specialisatie naar een concrete organisatie of sector
> gebeurt later en apart.

**Datum:** 2026-06-17 · **Status:** ontwerp goedgekeurd, blueprint nog te vullen via onderzoek

---

## 1. Probleem & ambitie

Het bestaande cisochat-concept is een *adviseur die práát*: een RAG-chatbot die vragen beantwoordt,
gegrond in BIO 2.0, ISO 27001/27701/22301 en AVG. Waardevol, maar smal.

De ambitie hier is breder: een vCISO die het werk *dóet* over de volle breedte van de CISO-rol —
strategie en beleid, risico, compliance, threat, posture, incident response en continuïteit. Niet
één monoliet, maar een **dirigent**: een redeneerlaag die het juiste instrument op het juiste moment
aanstuurt.

Dit ontwerp is bewust **generiek**. Het legt de architectuur en het capability-model vast zonder aan
één organisatie vast te zitten. De vertaling naar een specifieke context (hiërarchie, governance,
normenkader-invulling van een concrete organisatie) is een latere, aparte laag.

## 2. Kerngedachte: dirigent, geen doos

cisochat wordt het **vCISO-brein**: het redeneert langs een neutraal ordeningsframe, houdt grond in
normatieve kennis, en delegeert het uitvoerende werk naar gespecialiseerde componenten — bestaande
Commons-tools, herbruikbare AI-skills en externe open-source software.

```
                 ┌─────────────────────────────────────┐
   Gebruiker ──► │   cisochat = vCISO-dirigent          │
                 │   • NIST CSF 2.0 redeneerframe       │
                 │   • persona + advies (mens-in-loop)  │
                 │   • routing naar capability          │
                 │   • audit-trail by design            │
                 └───────────────┬─────────────────────┘
          ┌──────────────┬───────┼────────┬──────────────┐
          ▼              ▼        ▼        ▼              ▼
   kennisbank      grc-platform  security-  dreigings-/   externe OSS
   (RAG-grond)     (risk/controls) posture   kill-chain   (Prowler, OpenVAS,
                                  -tool      analyse       Wazuh, OWASP…)
          ▲                                                    ▲
          └────────── AI-skills (bio-map, nis2-iso,    ───────┘
                       risk-classification, audit-trail…)
```

### Leidende principes
- **AI adviseert, de mens beslist.** Nooit autonoom onomkeerbare acties (zoals het wijzigen van een
  risk-acceptatie of het versturen van een bestuurlijk stuk) zonder expliciete bevestiging.
- **Auditbaarheid by design.** Elke advies-/routing-stap is herleidbaar naar bron en redenering.
- **EU-soevereiniteit & open source als standaard** (Commons-principes).
- **Grounding boven geheugen.** Antwoorden steunen op opgehaalde normatieve bronnen, niet op
  trainingsdata.

## 3. Ordeningsframe: NIST CSF 2.0

De ruggengraat is **NIST CSF 2.0** met zes functies: **Govern · Identify · Protect · Detect ·
Respond · Recover**. Gekozen omdat het internationaal, framework-agnostisch en functioneel is, en
later 1-op-1 te mappen valt op BIO 2.0, ISO 27001:2022, NIS2 en AVG. Het houdt de generieke laag
neutraal; normenkader-specifieke mappings zijn een afgeleide laag.

| CSF-functie | vCISO-capabilities (generiek) |
|---|---|
| **Govern** | securitystrategie, beleid/policies, governance & rollen (RASCI), bestuurlijke rapportage |
| **Identify** | asset-/data-inventory, risk register & -beoordeling, threat modeling, compliance-mapping & gap-analyse |
| **Protect** | maatregelen-advies, awareness & cultuur, access/IAM-advies, configuratie-baselines |
| **Detect** | security posture & monitoring-advies, vulnerability management, detectie-engineering |
| **Respond** | incident-response-draaiboeken, coördinatie, communicatie naar stakeholders |
| **Recover** | continuïteit/BCM (ISO 22301), herstelplannen, lessons-learned |

## 4. De organen bestaan al — orkestratie boven herbouw

Commons heeft veel vCISO-organen al in huis. De vCISO-dirigent bouwt die niet opnieuw; hij stuurt ze
aan en vult de gaten.

| CSF-functie | Bestaand in Commons | Herbruikbare AI-skills | Externe OSS (kandidaten, te valideren) |
|---|---|---|---|
| Govern | `beleid-assistent`, `grc-platform` | generieke beleid-/rapportage-skills, `kpi-dashboard-design` | — |
| Identify | `grc-platform`, `dreigingsanalyse`, `kill-chain-analysis` | `risk-classification`, `ciso-bio-map`, `nis2-iso27001-mapping`, `ai-threat-modeling` | OpenCTI, MISP |
| Protect | `grc-platform` | `access-control-rbac`, `eu-ai-act-compliance` | OpenSCAP, policy-as-code |
| Detect | `security-posture-tool` | `vulnerability-scanning` | Prowler (MCP aanwezig), OpenVAS, Wazuh |
| Respond | — (gap) | `audit-trail-design` | TheHive, Cortex |
| Recover | — (gap) | — | — |
| Fundament | `kennisbank` (normatieve RAG-corpus) | `audit-trail-design` | — |

> De externe-OSS-kolom is **voorlopig** en wordt door het onderzoek (§6) gevalideerd en uitgebreid.

## 5. Componenten van de dirigent

1. **Redeneer-/persona-kern** — systeemprompt die de CISO-rol, het CSF-frame en de redeneerwijze
   definieert (adviserend, transparant over onzekerheid, nooit beslissend). Los van code zodat de
   community hem kan verbeteren.
2. **Grounding/RAG-laag** — ophalen van normatieve passages uit de `kennisbank` (BIO 2.0, ISO-normen,
   AVG, EU AI Act, IBD-richtlijnen) als context bij elk advies.
3. **Capability-router** — bepaalt per vraag welke CSF-functie en welke capability aan de orde is, en
   welk instrument (Commons-tool / skill / externe OSS) het werk levert.
4. **Mens-in-de-loop & audit-gate** — elke uitvoerende of onomkeerbare stap wordt eerst voorgelegd;
   elke stap wordt herleidbaar gelogd.
5. **Interface** — chat als één ingang; op termijn ingebed in of gekoppeld aan `grc-platform`.

## 6. Eerste deliverable: onderzoek + blueprint

Vóór er gebouwd wordt, leveren we een **diep en breed open-source-onderzoek** (via de
deep-research-harness: multi-source, fact-checked, met bronvermelding) dat de capability-map vult en
valideert. Resultaat is één blueprint-document in `cisochat/docs/` met:

- **OSS-landschap per capability** — welke open-source tools bestaan per CSF-functie (GRC, scanners,
  SIEM/SOAR, policy-as-code, threat-intel, awareness, BCM), beoordeeld op: rijpheid/onderhoud,
  licentie, EU-soevereiniteit/zelf-hostbaarheid, en integreerbaarheid (API/MCP).
- **Capability-map** — CSF-functie → capability → kandidaat-invulling (Commons-tool / AI-skill /
  externe OSS / nog-te-bouwen).
- **Gap-analyse** — wat ontbreekt of zwak is (nu zichtbaar: Respond en Recover) → voedt de roadmap.
- **Orkestratie-ontwerp** — hoe de dirigent capabilities aanroept, plus de mens-in-de-loop- en
  audit-grenzen.

## 7. Decompositie & realisatie

Dit is te groot voor één bouwslag. We faseren:

1. **Sub-project 1 (nu):** onderzoek + blueprint + roadmap. *(deze spec → plan → uitvoering)*
2. **Sub-project 2 e.v.:** per capability-cluster een eigen spec → plan → build, in CSF-volgorde van
   waarde. Verwachte startvolgorde: **Govern/Identify** eerst (daar staat `grc-platform` al), daarna
   Detect (`security-posture-tool` + externe scanners), dan de gaps Respond/Recover.

Elk later stuk doorloopt zijn eigen brainstorm-cyclus. We bouwen niet vóór de blueprint er is.

## 8. Huis, regime & muren

- **Woont in:** `X:\SECURITY-COMMONS-NL\cisochat\` — eigen git-repo, open source, EU-soeverein.
- **Regime:** open (Commons).
- **Muur-check:**
  - ✅ Generiek/open source — **geen** organisatie-specifieke of tenant-content in deze laag. De
    specialisatie naar een concrete organisatie gebeurt later, apart, binnen het eigen domein van die
    organisatie.
  - ⚠️ **LIVIQ ⟷ Commons licentie-grens:** geen proprietary LIVIQ-IP in de open-source blueprint
    mengen. Open-core-keuzes bewust maken, niet sluipenderwijs.

## 9. Wat dit niet is

- Geen vervanging van een echte CISO of FG, en geen juridisch advies.
- Geen autonoom beslissend systeem — adviserend, mens-in-de-loop.
- Geen systeem dat data buiten de EU verzendt.
- Geen monoliet die alles zelf herbouwt — een dirigent boven bestaande organen.

## 10. Open punten voor het plan

- Concrete deep-research-vraagstelling en bronnenstrategie (welke catalogi/lijsten als startpunt).
- Beoordelingscriteria voor OSS-tools operationaliseren (scorekaart).
- Mechanisme van de capability-router: prompt-routing vs. expliciete tool-aanroepen (MCP) — te
  bepalen na het OSS-onderzoek.
