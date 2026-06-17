# vCISO-blueprint — OSS-landschap, capability-map, gaps & orkestratie

> **Wat dit is.** De synthese van het open-source-onderzoek (zeven sweeps: zes NIST CSF 2.0-functies +
> een cross-cutting AI-vCISO-sweep) tot één generieke blueprint voor de vCISO-dirigent in `cisochat`.
> Generiek en framework-agnostisch; specialisatie naar een concrete organisatie komt later en apart.
>
> **Status:** **vastgesteld** (2026-06-17, na mens-in-de-loop review + steekproef-verificatie van de
> zwaarst-wegende bronnen — zie noot onderaan). **Peildatum onderzoek:** juni 2026.
> **Bronnen:** de zeven `research/*.md`-bestanden in deze map; alle tool-claims daar zijn voorzien van
> bron-URL's. **Harde poort:** alleen OSI-open source; source-available (BSL/SSPL/ELv2/CC-NC/custom) en
> proprietary "community"-edities zijn uitgesloten en als zodanig geflagd.
>
> **Reikwijdte-keuze.** cisochat is in deze blueprint een **standalone-orkestrator** van externe OSS + een
> eigen advies-brein (RAG op de normatieve `kennisbank`). We bouwen géén harde afhankelijkheid op andere
> Security-Commons-projecten; hoe cisochat zich conceptueel tot die projecten verhoudt staat in §6.

---

## §1 — OSS-landschap per CSF-functie (top-kandidaten)

Per functie de volwassen open-source top-kandidaten. Volledige scorekaarten + de long tail staan in het
bijbehorende `research/<functie>.md`. Legenda fit-score: 5 = rijp/permissief/EU-soeverein/AI-native;
3 = bruikbaar met één serieus bezwaar; 1 = bestaat maar nauwelijks bruikbaar.

### Govern → `research/govern.md`
| Tool | Fit | Licentie | EU | Integratie | AI-native |
|---|---|---|---|---|---|
| CISO Assistant | 5 | AGPL-3.0 | ✅ (FR) | REST/CLI | deels (lokale LLM, geen MCP) |
| Cedar | 5 | Apache-2.0 | ✅ | CLI/lib/Wasm | ja (cedar-for-agents, MCP) |
| OPA | 5 | Apache-2.0 | ✅ | CLI/REST/lib | deels (3rd-party MCP) |
| Probo | 4 | MIT | ✅ | GraphQL/CLI | **ja (MCP, 270+ tools)** |
| Kyverno | 4 | Apache-2.0 | ✅ | CLI/K8s-API | deels |

### Identify → `research/identify.md`
| Tool | Fit | Licentie | EU | Integratie | AI-native |
|---|---|---|---|---|---|
| NetBox (asset/CMDB) | 5 | Apache-2.0 | ✅ | REST/GraphQL | deels |
| CISO Assistant (compliance-mapping/gap) | 5 | AGPL-3.0 | ✅ | REST | deels |
| MISP (CTI) | 5 | AGPL-3.0 | ✅ (EU-oorsprong) | REST/feeds | deels |
| MONARC (risk) | 4 | AGPL-3.0 | ✅ (LU/EU) | REST | nee |
| OWASP Threat Dragon / Threagile (threat modeling) | 4 | Apache-2.0 | ✅ | CLI/desktop | deels |
| OpenCTI (CTI) | 4 | Apache-2.0 (open-core) | ✅ | GraphQL | deels |

### Protect → `research/protect.md`
| Tool | Fit | Licentie | EU | Integratie | AI-native |
|---|---|---|---|---|---|
| Keycloak (IAM) | 5 | Apache-2.0 | ✅ | REST/OIDC | nee |
| OpenSCAP + ComplianceAsCode (hardening) | 5 | LGPL/diverse | ✅ | CLI/lib | nee |
| OPA (policy-enforcement) | 5 | Apache-2.0 | ✅ | CLI/REST | deels |
| authentik (IAM) | 4 | MIT | ✅ | REST | nee |
| Lynis · dev-sec.hardening | 4 | GPL/MIT | ✅ | CLI/Ansible | nee |
| Gophish (phishing-sim) | 3 | MIT | ✅ | REST | nee (⚠️ stagnant sinds 2022) |

### Detect → `research/detect.md`
| Tool | Fit | Licentie | EU | Integratie | AI-native |
|---|---|---|---|---|---|
| Wazuh (SIEM/XDR) | 5 | GPL-2.0 | ✅ | REST | nee (OSS-editie) |
| Prowler (CSPM) | 5 | Apache-2.0 | ✅ | CLI/REST/**MCP** | **ja (Lighthouse)** |
| OWASP Dependency-Track (vuln/SBOM) | 5 | Apache-2.0 | ✅ | REST | deels |
| Sigma · YARA-X (detection-as-code) | 5 | DRL/BSD | ✅ | CLI/lib | deels |
| Greenbone/OpenVAS (vuln) | 4 | GPL | ✅ (DE) | REST | nee |
| Trivy (vuln/IaC) | 4 | Apache-2.0 | ✅ | CLI/lib | deels (⚠️ supply-chain-incident mrt 2026 → pin hashes) |

### Respond → `research/respond.md`
| Tool | Fit | Licentie | EU | Integratie | AI-native |
|---|---|---|---|---|---|
| DFIR-IRIS (case mgmt) | 5 | LGPL-3.0 | ✅ | REST | nee |
| Shuffle (SOAR) | 5 | AGPL/MIT | ✅ | REST | deels |
| Tracecat (SOAR) | 4 | AGPL (open-core) | ✅ | REST/**MCP** | **ja (AI-agents)** ⚠️ beta |
| CACAO v2 + SOARCA (playbook-standaard) | 4 | Apache-2.0 | ✅ (NL/EU) | API | deels |
| Velociraptor (endpoint-respons, multi-functie) | 4 | AGPL-3.0 | ✅ | API/VQL | nee |
| Cortex (analyzer) | 3 | AGPL-3.0 | ✅ | REST | nee (tempo zakt) |

> ⚠️ **TheHive 5 uitgesloten** — proprietary sinds 2022; AGPL-versies (v3/v4) end-of-life. De-facto OSS-opvolger = DFIR-IRIS.

### Recover → `research/recover.md`
| Tool | Fit | Licentie | EU | Integratie | AI-native |
|---|---|---|---|---|---|
| restic (backup) | 5 | BSD-2 | ✅ | CLI/JSON | nee |
| Velero (K8s backup/DR) | 5 | Apache-2.0 | ✅ | K8s-API/CLI | deels |
| BorgBackup (backup) | 4 | BSD-3 | ✅ | CLI | nee |
| LitmusChaos (DR-testing) | 4 | Apache-2.0 | ✅ | CRD/GraphQL/**MCP** | **ja (Litmus MCP)** |
| CISO Assistant (ISO 22301/BIA-check) | 3 | AGPL-3.0 | ✅ | REST | deels |
| OneUptime (postmortem-module) | 3 | Apache-2.0 | ✅ | REST | deels |

### Cross-cutting — AI-vCISO / orkestratie-bouwstenen → `research/ai-vciso-meta.md`
| Project | Fit | Licentie | Waarvoor (herbruikbaar als) |
|---|---|---|---|
| CISO Assistant | 5 | AGPL-3.0 | GRC-ruggengraat (backend via REST/MCP) |
| Anthropic Cybersecurity Skills ⚠️ | 5 | Apache-2.0 | kennislaag-**patroon** (754 skills, progressive disclosure) — ⚠️ **community-repo (@mukul975), niet Anthropic-officieel**; gebruik het patroon, niet de naam |
| Microsoft Agent Governance Toolkit | 4 | MIT | **deterministisch policy-enforcement** voor de noorderster/routing-gate; Merkle-audit |
| AiSOC | 4 | MIT | multi-agent SOC-architectuur; **Investigation Ledger** (audit-by-design); gelaagd geheugen |
| Prowler Lighthouse | 4 | Apache-2.0 | patroon **MCP-als-domeininterface** |
| STRIDE-GPT | 4 | MIT | AI-threat-modeling; twee-tier model-routing |
| NIST CSF 2.0 MCP Server | 3 | MIT | CSF-framework als MCP-tool (assessment/gap) |
| ITBench CISO-CAA Agent | 3 | Apache-2.0 | NL→policy-generatie; benchmark (25% autonomie-plafond) |

---

## §2 — Capability-map

Per CSF-functie: de vCISO-capability → hoe die wordt ingevuld. Kolom **invulling** kent vier types:
**[OSS]** externe open-source tool · **[Skill]** generieke AI-skill/kennislaag · **[Brein]** = *reasoning + RAG,
géén tool* (het advies-brein van de dirigent) · **[Bouwen]** nog te bouwen (gap → roadmap).

> **Cruciaal — het advies-brein.** De **[Brein]**-capabilities zijn het hart van de vCISO: oordeel, afweging,
> vertaling naar bestuur. Daar is geen tool voor en hoort er ook geen te zijn — dit is de dirigent zelf,
> gegrond (RAG) in de normatieve `kennisbank`. De catalogus eromheen levert feiten en uitvoering; het brein
> weegt en adviseert. Mens beslist (Noorderster).

### Govern
| Capability | Invulling |
|---|---|
| Securitystrategie formuleren | **[Brein]** (RAG op normen/sector) — geen OSS; advies-werk |
| Beleid/policy-lifecycle (geschreven) | **[OSS]** CISO Assistant (beleidsmodule) + **[Brein]** redactie/afweging — *jonge module, gap in acknowledgement-tracking* |
| Policy-as-code | **[OSS]** OPA · Kyverno · Cedar |
| Governance & rollen (RASCI) | **[Bouwen]** — bevestigde OSS-gap; nu **[Brein]** + wiki/GRC-eigenaarschap |
| Bestuurlijke rapportage / KPI | **[OSS]** Grafana-feed (op GRC-data) + **[Brein]** duiding voor bestuur — *geen kant-en-klare "board-view" OSS* |
| ISMS/GRC-governancelaag | **[OSS]** CISO Assistant (ruggengraat) |

### Identify
| Capability | Invulling |
|---|---|
| Asset-/data-inventory | **[OSS]** NetBox · Ralph |
| Risk register & -beoordeling | **[OSS]** MONARC / CISO Assistant + **[Brein]** risico-interpretatie & -prioritering |
| Threat modeling | **[OSS]** Threat Dragon · Threagile · pytm + **[Skill]** STRIDE-GPT-patroon + **[Brein]** |
| Compliance-mapping & gap-analyse | **[OSS]** CISO Assistant · NIST CSF MCP-server + **[Skill]** norm-mapping (BIO2/ISO/NIS2) |
| Threat intelligence | **[OSS]** MISP · OpenCTI |

### Protect
| Capability | Invulling |
|---|---|
| Control-/maatregelenbeheer | **[OSS]** CISO Assistant |
| Maatregel-advies & afweging | **[Brein]** (maatregel vs. restrisico) |
| Awareness & phishing-simulatie | **[OSS]** Gophish (⚠️ stagnant) + **[Bouwen]** OSS-awareness-content |
| IAM / access-governance | **[OSS]** Keycloak · authentik |
| Configuratie-baselines & hardening | **[OSS]** OpenSCAP+ComplianceAsCode · Lynis · dev-sec |
| Policy-as-code-enforcement | **[OSS]** OPA · Kyverno (zie Govern) |

### Detect
| Capability | Invulling |
|---|---|
| Security posture / CSPM | **[OSS]** Prowler (MCP) |
| Vulnerability management | **[OSS]** Greenbone/OpenVAS · Trivy · OWASP Dependency-Track |
| SIEM / monitoring | **[OSS]** Wazuh · OpenSearch Security Analytics |
| Detection-as-code | **[OSS]** Sigma · YARA-X |
| Detectie-prioritering/duiding | **[Brein]** (false-positive-weging, escalatie-advies) |

### Respond
| Capability | Invulling |
|---|---|
| Incident response & case management | **[OSS]** DFIR-IRIS |
| SOAR / playbook-automatisering | **[OSS]** Shuffle · Tracecat (beta) |
| IR-coördinatie & besluitvorming | **[Brein]** (mens-in-de-loop) |
| Playbook-standaarden | **[OSS]** CACAO v2 + SOARCA |
| Crisiscommunicatie | **[Brein]** opstellen + **[Bouwen]** — EU-soevereine OSS-comms-gap |

### Recover
| Capability | Invulling |
|---|---|
| Backup & herstel-orchestratie | **[OSS]** restic · BorgBackup · Velero (K8s) |
| DR-testing / veerkracht | **[OSS]** LitmusChaos · Chaos Toolkit |
| BCM / ISO 22301-lifecycle | **[Bouwen]** — ernstige OSS-gap; nu CISO Assistant als compliance-check |
| BIA | **[Bouwen]** — ernstige OSS-gap; nu spreadsheet/CISO Assistant |
| DR-planning & runbook-orchestratie | **[Bouwen]** — ernstige OSS-gap |
| Post-incident review / lessons-learned | **[OSS]** OneUptime (module) + **[Brein]** synthese + **[Bouwen]** dedicated postmortem |

### Cross-cutting (de dirigent zelf)
| Capability | Invulling |
|---|---|
| Normatieve grounding (BIO2/ISO/NIS2/AVG/EU AI Act) | **[Skill]** RAG op de normatieve `kennisbank` (corpus, geen tool-afhankelijkheid) + **[Brein]** |
| Kennis-/skill-laag | **[Skill]** progressive-disclosure-patroon (vgl. Anthropic Cybersecurity Skills ⚠️ community-repo, niet Anthropic) + eigen skills |
| Routing & policy-gate (Noorderster) | **[OSS-patroon]** Microsoft AGT (deterministisch) + **[Bouwen]** |
| Auditspoor | **[OSS-patroon]** AiSOC Investigation Ledger / AGT Merkle-audit + append-only beslislog |

### Cross-functie-reconciliatie (dedup)
Tools die in meerdere sweeps opdoken — één canonieke entry, alle functies, afgestemde score:
| Tool | Canonieke fit | Dekt functies |
|---|---|---|
| CISO Assistant | 5 | Govern (primair) · Identify · Protect · Recover (ISO 22301) |
| Prowler | 5 | Detect (primair) · Identify · Govern (rapportage) |
| Wazuh | 5 | Detect (primair) · Protect (SCA) · Govern (compliance-views) · Respond |
| OPA / Kyverno / Cedar | 5/4/5 | Govern (beleid) · Protect (enforcement) |
| Trivy | 4 | Detect (primair) · Identify · Protect (IaC) |
| OpenCTI / MISP | 4/5 | Identify (primair) · Detect |
| Velero · DRBD | 5/— | Recover (primair) · Protect (data-bescherming) |
| OneUptime · Velociraptor | 3/4 | Respond (primair) · Recover |

---

## §3 — Gap-analyse (voedt de roadmap)

Per functie wat ontbreekt of zwak is in volwassen OSS (bron: de "Niet-gedekt"-paragrafen).

- **Govern.** Grootste gap = **RASCI/verantwoordelijkheidsgovernance** (geen volwassen OSS; alleen
  enkelvoudige eigenaarschap-velden in GRC). Verder: geen kant-en-klare **bestuurlijke KPI-board-view**;
  beleids-**acknowledgement-tracking** ontbreekt OSS-breed; rijpe-én-MCP-native GRC bestaat nog niet in
  één tool (keuze: CISO Assistant rijp-zonder-MCP vs. Probo MCP-native-maar-jonger).
- **Identify.** Geen rijp OSS **OpenFAIR**-kwantitatief-risicoplatform; geen volwassen **OT/ICS**-asset-
  discovery; SBOM→risk-register vergt maatwerk; AI-governance-tooling (EU AI Act) embryonaal.
- **Protect.** **DLP/data-discovery** (hoge gap), NAC/microsegmentatie, **secrets-management** (Vault is
  BSL → OpenBao-fork), en OSS-**awareness-content** (geen open SCORM-content) ontbreken.
- **Detect.** Geen rijp OSS **NDR**, **UEBA**, **AI-native SIEM** of **ITDR**; sterke Windows-bias in
  endpoint-detectie.
- **Respond.** Geen volwassen, security-eerst, **EU-soevereine crisiscommunicatie-OSS** (leunt op
  US-SaaS/Slack of generieke statuspagina's).
- **Recover (dunste functie).** Ernstige gaten in **BCM-lifecycle-management**, **BIA-tooling**,
  **DR-planning/runbook-orchestratie** en **dedicated postmortem-management**. Backup/DR-testing is wél
  ruim gedekt.

**Rode draad:** de **technische/uitvoerende** kant (scanners, SIEM, backup, IAM, policy-as-code) is rijk
in OSS; de **governance-/proces-/advieskant** (RASCI, BCM, BIA, bestuurlijke KPI, crisiscommunicatie,
postmortem-proces) is dun. Dat bevestigt de kerngedachte: **de meeste vCISO-waarde van `cisochat` zit niet
in nóg een tool, maar in het advies-brein + de orkestratie dáár waar OSS-tooling ontbreekt.**

---

## §4 — Orkestratie-ontwerp

Hoe de dirigent (`cisochat`) een vraag afhandelt, onderbouwd met de integreerbaarheid-/AI-native-bevindingen
en de "Lessen voor de dirigent-architectuur" uit `ai-vciso-meta.md`.

> 📊 **Visuele weergave:** zie [`architectuur.html`](architectuur.html) — interactieve plaat met drie views
> (hoe een vraag stroomt · gelaagde architectuur · CSF-capability-map).

### Routeringsflow
1. **CSF-functie-detectie** (LLM-classificatie): valt de vraag onder Govern/Identify/.../Recover, of is het
   puur advies?
2. **Capability-routing**: welke capability uit §2, en welk invullingstype ([OSS]/[Skill]/[Brein]/[Bouwen]).
3. **Instrumentkeuze**: bij **[Brein]** → redeneren + RAG op de `kennisbank`; bij **[OSS]** → het
   instrument aanroepen; bij **[Bouwen]** → eerlijk melden dat er (nog) geen volwassen invulling is.

### Router-mechanisme — beslissing
**Hybride, met een deterministische gate vooraan.** Onderbouwing uit het onderzoek:
- **Prompt-routing** (LLM) voor de zachte stappen: CSF-classificatie, capability-keuze, advies-synthese.
- **Expliciete tool-aanroepen via MCP** waar beschikbaar — het onderzoek toont een groeiend MCP-aanbod
  (Prowler Lighthouse, Probo, NIST CSF MCP-server, Litmus, CoPilot, AiSOC). Voor rijpe tools zónder MCP
  (CISO Assistant, Wazuh, Keycloak) een **REST/CLI-adapter**. Het patroon **MCP-als-domeininterface**
  (Prowler) is leidend: kapsel elk domein in achter een uniforme interface, herschrijf de tool niet.
- **MCP-laag model-agnostisch** houden (Ollama/LM Studio/Mistral) voor EU-soevereiniteit.
- **Progressive disclosure** voor de kennis-/skill-laag (Anthropic-Cybersecurity-Skills-patroon, ⚠️ het
  patroon — niet de community-repo zelf): kleine routing-header eerst, vol protocol alleen bij match.

Dit beantwoordt het open punt uit de ontwerp-spec (§10): **geen monolithische agent en geen pure
prompt-routing, maar een dirigent die per CSF-functie het juiste MCP/REST-instrument aanstuurt, met
LLM-routing ervoor en een deterministische gate eronder.**

### Mens-in-de-loop & audit (de Noorderster, technisch)
- **Deterministisch policy-enforcement, geen LLM-guardrail** (les van Microsoft AGT, geverifieerd: het
  toolkit citeert Andriushchenko et al. (ICLR 2025) met 100% attack success op GPT-4o/Claude 3/Llama-3).
  De **routing-gate** is een harde, code-niveau check vóór elke schrijf-/onomkeerbare actie — niet het
  model dat "nee" zegt. Dit is de technische vertaling van "AI bereidt voor, de mens beslist".
- **Audit-by-design**: elke prompt, tool-aanroep, bron en beslissing in een herleidbaar spoor
  (AiSOC Investigation Ledger / AGT Merkle-audit als blauwdruk; een append-only beslislog als semantisch
  equivalent).
- **Realistische autonomie**: ITBench toont ~25% autonome oplossing van CISO-scenario's. De dirigent is
  **decision-support & voorbereiding**, niet autonoom uitvoerder — focus op de ~75% voorbereidings-,
  analyse- en documentatietaken.

---

## §5 — Roadmap (gefaseerde bouw, sub-project 2 e.v.)

Volgorde van waarde, afgeleid uit de gap-analyse. Elke fase is een eigen brainstorm → spec → plan-cyclus.

**Fase A — Fundament & dirigent-skelet (hoogste prioriteit).**
De kennis-/grounding-laag (`kennisbank` + RAG), de capability-router, en de **deterministische routing-gate +
auditspoor** (AGT/AiSOC-patronen). Dit is de kern waar al het andere op leunt; een append-only beslislog
vormt het semantische auditspoor.

**Fase B — Govern/Identify eerst (sterkste OSS-basis).**
Koppel CISO Assistant als GRC-backend via MCP/REST; integreer compliance-mapping (norm-mapping BIO2/ISO/NIS2),
threat-intel (MISP/OpenCTI) en threat-modeling (STRIDE-GPT-patroon). Bouw de **RASCI-laag** (bevestigde gap)
als lichte module bovenop de GRC-API.

**Fase C — Detect (rijpe OSS).**
Prowler (MCP) + Wazuh + Dependency-Track als detect-instrumenten; detectie-duiding via het brein.

**Fase D — Govern-rapportage & advies-brein verdiepen.**
Bestuurlijke KPI-view (GRC-data → Grafana → brein-duiding) en beleids-lifecycle-ondersteuning.

**Fase E — Respond & de gaps (Recover).**
DFIR-IRIS + Shuffle aanhaken; daarna de zware gaps aanpakken waar OSS ontbreekt: **BCM/BIA-lichtgewicht
module**, **crisiscommunicatie**, **postmortem-proces** — kandidaten voor eigen bouw, want hier vult
`cisochat` een echt marktgat.

> **Leidend principe door alle fasen:** bouw geen slechter alternatief naast bestaande rijpe OSS — koppel
> en orkestreer. Bouw zelf alleen waar de gap-analyse een echt gat aantoont (RASCI, BCM/BIA, crisiscomms,
> postmortem-proces, bestuurlijke KPI-view).

---

## §6 — Positionering binnen Security Commons NL

> README-klare tekst: hoe `cisochat` zich verhoudt tot de overige Security-Commons-projecten — zónder er een
> harde technische afhankelijkheid van te maken.

Security Commons NL is een verzameling **instrumenten**: elk project doet één security-taak goed — GRC/ISMS,
posture-meting, dreigings- en kill-chain-analyse, beleidsondersteuning, weerbaarheidstraining, een kennisbank.

`cisochat` is geen extra instrument in die rij — het is de **dirigent**: het redenerende CISO-brein dat
*eroverheen* denkt. Waar de andere projecten een taak uitvoeren, weegt cisochat langs NIST CSF 2.0 af,
grondt zich in de normen (RAG), adviseert, en stuurt — waar nodig — het juiste instrument aan. Mens beslist.

- **Standalone, niet afhankelijk.** Wie alleen cisochat draait, heeft een werkende vCISO-adviseur die externe
  open-source tooling én zijn eigen advies-brein orkestreert. cisochat bouwt geen harde koppeling op andere
  Commons-projecten.
- **Wel complementair.** Wie óók andere Commons-tools draait, geeft de dirigent rijkere instrumenten om mee
  te werken. De verhouding is "dirigent ↔ instrumenten", niet "onderdeel van een suite".

**Eén-zin-pitch (README):** *"Waar de andere Security-Commons-projecten elk één security-taak uitvoeren, is
cisochat het redenerende CISO-brein dat eroverheen denkt — adviserend, gegrond in de normen, mens beslist."*

---

## Vervolg

Sub-project 1 (onderzoek + blueprint) is **vastgesteld**. Reviewbesluiten verwerkt: bronnen-steekproef ✅,
router-mechanisme + bouwvolgorde akkoord, geen harde Commons-afhankelijkheid, positionering vastgelegd (§6).
Volgende stap = **sub-project 2 (Fase A: fundament & dirigent-skelet)** als eigen brainstorm-cyclus.

### Verificatie-noot (2026-06-17)
Steekproef op de zwaarst-wegende claims, alle bevestigd: **CISO Assistant** (AGPL-3.0 + intuitem-commercieel,
FR, 4,1k★, v3.18.1) · **Microsoft Agent Governance Toolkit** (MIT, 4,4k★, LLM-guardrail-faalclaim gegrond in
Andriushchenko et al. ICLR 2025) · **Eramba** (terecht buiten de poort: niet-OSI) · **TheHive 5** (terecht
uitgesloten: proprietary sinds 2021/22; DFIR-IRIS = OSS-opvolger) · **Anthropic Cybersecurity Skills**
(bestaat, Apache-2.0, 16,1k★ — maar ⚠️ community-repo @mukul975, *niet* Anthropic-officieel).
