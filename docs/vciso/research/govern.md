# GOVERN — open-source tooling landscape (NIST CSF 2.0)

> **Scope.** Dit document inventariseert open-source tooling voor de NIST CSF 2.0-functie **GOVERN** (GV)
> ten behoeve van een generieke, framework-agnostische vCISO-blueprint. De functie GOVERN omvat
> securitystrategie & beleidsbeheer, governance-rollen & verantwoordelijkheidstoewijzing (RASCI),
> bestuurlijke rapportage & risk-/KPI-dashboards, en de ISMS/GRC-governancelaag. Per sub-categorie
> zijn de **top 2–3 tools** volledig uitgewerkt (12-velden scorekaart); overige vondsten staan als
> *long tail* (naam + URL + 1 zin). Harde poort: **alléén open source** — open-core wordt beoordeeld
> op uitsluitend de community-editie, met expliciete vermelding van wat achter de betaalmuur zit.
> EU-soevereiniteit is een zachte weging (zelf-hostbaarheid + dataresidentie). Alle tool-claims zijn
> voorzien van ≥1 bron-URL. Peildatum onderzoek: **juni 2026**.
>
> **Let op — terminologische val:** "policy management" betekent in GOVERN twee verschillende dingen.
> (a) *beleidsbeheer* = lifecycle van geschreven beleidsdocumenten (draft → review → approve → publish),
> en (b) *policy-as-code* = machine-afdwingbare regels (OPA/Kyverno). Beide zijn hieronder apart behandeld.

---

## 1. ISMS / GRC-governancelaag

Dit is de ruggengraat van GOVERN: het bewaren van het ISMS, het koppelen van controls aan frameworks,
en het dragen van risk-, audit- en compliance-governance. Twee tools domineren de open-source ruimte;
de rest is óf open-core met dunne community-editie, óf minder actief.

### 1.1 CISO Assistant (intuitem) — *primaire aanbeveling GOVERN-breed*

1. **Naam + URL:** CISO Assistant — https://github.com/intuitem/ciso-assistant-community
2. **CSF-functie(s):** GOVERN (primair), met doorwerking naar IDENTIFY (risk assessment) en — via beleids-/auditmodules — alle functies. Multi-framework mapping over de hele CSF.
3. **Capability:** ISMS/GRC-governance, beleidsbeheer (lifecycle), framework- & control-mapping, risk-governance, compliance-rapportage. Dekt het grootste deel van GOVERN in één tool.
4. **Omschrijving:** API-first GRC-platform dat 150+ frameworks ondersteunt (ISO 27001, NIST CSF 2.0, NIS2, DORA, BIO2, SOC 2, CIS, NIST AI RMF, GDPR) met automatische control-mapping en multi-framework-evaluatie van één scope. Sinds v3.14 (maart 2026) ook een native markdown-beleidseditor met lifecycle-states.
5. **Rijpheid:** **HOOG.** v3.18.1 (15 juni 2026); 272 releases, ~7.464 commits, ~4.100 sterren, actieve release-cadans (meerdere minors/maand). Geprezen in onafhankelijke reviews als snelst bewegende OSS-GRC.
6. **Licentie:** **AGPL-3.0** voor de community-editie (alles buiten de `enterprise/`-directory); de `enterprise/`-map valt onder een proprietary "intuitem Commercial Software License". Copyleft-implicatie: netwerk-copyleft (AGPL) — eigen wijzigingen die je als dienst aanbiedt moeten ook onder AGPL beschikbaar zijn. **Open-core:** enterprise-editie voegt o.a. SSO/SAML, multi-tenancy en geavanceerde rapportage toe; de community-editie is functioneel volwaardig voor één organisatie.
7. **EU-soevereiniteit:** **STERK.** Zelf-hostbaar via Docker/Docker-Compose (PostgreSQL of SQLite, S3/Azure-Blob optioneel, Caddy meegeleverd). Geen verplichte cloud, geen data buiten EU nodig. Leverancier intuitem is Europees (FR).
8. **Integreerbaarheid:** **API + CLI + UI.** REST API met Swagger UI, token-auth, endpoints voor alle objecten ("API-first to support both UI interaction and external automation"). Goed koppelbaar aan een AI-dirigent.
9. **AI-native koppelbaarheid:** **DEELS → ja.** Lokale LLM-engine gedocumenteerd in de backend-chat-module; ondersteunt NIST AI RMF als governance-framework. Schone REST-API en gestructureerde output maken het agent-vriendelijk; (nog) geen dedicated MCP-server.
10. **Stack/taal:** Python/Django (backend), Svelte + TypeScript (frontend); PostgreSQL/SQLite; Docker/Gunicorn/Caddy.
11. **Fit-score:** **5/5** — rijp, actief, EU-soeverein zelf-hostbaar, API-first met lokale-LLM-haakjes; dekt de meeste GOVERN-capabilities in één tool. (Enige minpunt: AGPL-copyleft vergt aandacht bij eigen forks-as-a-service.)
12. **Bronnen:** https://github.com/intuitem/ciso-assistant-community · https://intuitem.com/whats-new-ciso-assistant-2026-w11/ · https://www.helpnetsecurity.com/2026/01/14/ciso-assistant-open-source-cybersecurity-management-grc/ · https://infosecflow.com/blog/open-source-grc-comparison/

### 1.2 Probo (getprobo) — *MCP-native open-source GRC*

1. **Naam + URL:** Probo — https://github.com/getprobo/probo
2. **CSF-functie(s):** GOVERN (compliance-/control-governance), met beleids- en auditondersteuning.
3. **Capability:** ISMS/GRC-governance (compliance-management, controls, vendor-risk), met een uitgesproken AI-/MCP-koppelvlak.
4. **Omschrijving:** Moderne open-source compliance-/GRC-tool (Vanta/Drata-alternatief) met een GraphQL-API én een MCP-server met 270+ tools, plus een `prb` CLI — gebouwd om door AI-assistenten (Claude/Cursor/Continue) aangestuurd te worden.
5. **Rijpheid:** **MIDDEN-HOOG.** v0.210.0 (16 juni 2026), ~1.2k sterren, zeer actieve release-cadans; jonger en kleiner dan CISO Assistant maar duidelijk gefinancierd/onderhouden.
6. **Licentie:** **MIT/ISC** (permissief, geen copyleft). Geen waargenomen betaalde tier — voor zover gevonden volledig open source (verifieer dit zelf vóór adoptie, want het ecosysteem verandert snel).
7. **EU-soevereiniteit:** **STERK.** Zelf-hostbaar via Docker; geen verplichte cloud.
8. **Integreerbaarheid:** **GraphQL-API + MCP + CLI (`prb`).** Het meest expliciet voor automatisering ontworpen GRC-platform in deze set.
9. **AI-native koppelbaarheid:** **JA (sterkst in deze categorie).** Eigen MCP-server met 270+ tools, getest met Claude/Cursor/Continue — direct koppelbaar aan een AI-dirigent zonder eigen integratielaag.
10. **Stack/taal:** Go + TypeScript (GraphQL); Docker.
11. **Fit-score:** **4/5** — permissief, EU-soeverein, uniek MCP-native; afgewaardeerd t.o.v. CISO Assistant op rijpheid/framework-breedte (kleiner, jonger, smallere framework-dekking).
12. **Bronnen:** https://github.com/getprobo/probo · https://github.com/getprobo/awesome-compliance

### 1.3 Eramba (Community Edition) — *let op: licentie betwist*

1. **Naam + URL:** Eramba Community Edition — https://www.eramba.org (Docker-helpers: https://github.com/eramba/docker; oude onofficiële mirror: https://github.com/sys02/eramba)
2. **CSF-functie(s):** GOVERN (primair: beleid, control-, risk- en auditgovernance).
3. **Capability:** ISMS/GRC-governance, beleidsbeheer met review-cyclus, control- & compliance-management, interne audits.
4. **Omschrijving:** Gevestigd GRC-platform (sinds 2007) met sterke documentdiscipline: policies/standards/procedures met approval-workflow, automatische review-records per deadline, publieke policy-portal en framework-koppeling van controls.
5. **Rijpheid:** **MIDDEN-HOOG.** Actief onderhouden (v3.30.0 ~mei 2026), volwassen featureset.
6. **Licentie:** **⚠️ BETWIST / onduidelijk.** De officiële Eramba-org publiceert **geen broncode-repo** — alleen Docker-deployment-helpers. De community-editie is gratis maar feitelijk **closed-source/proprietary** in de OSI-betekenis; het enige GPLv2-bewijs is een oude *onofficiële* mirror (`sys02/eramba`, 1 ster), niet de levende codebase. **Behandel Eramba daarom met voorzichtigheid: niet aantoonbaar OSI-open source.** Enterprise-editie: €5.000/jaar.
7. **EU-soevereiniteit:** **STERK (deployment).** Zelf-hostbaar via Docker; geen verplichte cloud — maar de closed-source-status ondermijnt het soevereiniteitsvoordeel (geen broncode-controle).
8. **Integreerbaarheid:** **API aanwezig**, maar in de community-editie beperkt; volledige API/automatisering grotendeels enterprise.
9. **AI-native koppelbaarheid:** **DEELS.** Eramba noemt "LLM Integration" als feature, maar zonder open broncode is dit niet onafhankelijk verifieerbaar en niet als OSS-MCP gedocumenteerd.
10. **Stack/taal:** PHP (CakePHP), MySQL, Docker.
11. **Fit-score:** **2/5** — functioneel volwassen en EU-host­baar, maar **één diskwalificerend bezwaar voor deze blueprint: niet aantoonbaar OSI-open source** (officiële broncode ontbreekt). Genoemd voor volledigheid; niet aanbevolen onder de harde open-source-poort.
12. **Bronnen:** https://github.com/eramba/docker · https://eramba.org · https://grc-review.com/products/eramba

### Long tail — ISMS/GRC

- **SimpleRisk** — https://github.com/simplerisk/simplerisk — **MPL-2.0** core (echt open source), actief (release 20260519, juni 2026); core risk-register/scoring + dashboards gratis met onbeperkte users, **maar API, AI, Jira, import/export en incident-mgmt zitten achter betaalde "Extras" (Standard $5k/jr, Premium $10k/jr)** — duidelijke open-core.
- **deming (sourcentis)** — https://github.com/sourcentis/deming — **GPL-3.0**, volledig OSS, actief (release 2026.06.16, ~383 sterren); klassieke ISMS-tool, **maar geen API en geen AI** → lastig aan een AI-dirigent te koppelen.
- **theopenlane/core** — https://github.com/theopenlane/core — **Apache-2.0** OSS-core (~261 sterren, v1.23.12 juni 2026) met GraphQL + `openlane` CLI; hybride model (betaalde cloud-console).
- **unidoc/isms** — https://github.com/unidoc/isms — **Apache-2.0**, AI-first/git-native ISMS met **MCP-server (22 tools)** + REST + CLI (single binary); **nog zeer pril** (~6 sterren, v0.6.0 juni 2026) → veelbelovend maar onrijp.
- **unicis-platform-ce** — https://github.com/UnicisTech/unicis-platform-ce — Apache-2.0 CE (Vanta/Drata-alternatief), TypeScript; jong (~93 sterren).
- **OpenGRC (LeeMangold)** — https://github.com/LeeMangold/OpenGRC — Laravel-GRC; **let op: CC BY-NC-SA 4.0 (source-available, NIET OSI-open) — commercieel hosten/resale verboden.** (De `OpenGRC/OpenGRC`-URL bestaat niet; juiste repo is `LeeMangold/OpenGRC`.)
- **VerifyWise** — https://github.com/verifywise-ai/verifywise — **BSL-1.1 (source-available, niet OSI)**, AI-governance-focus (EU AI Act/ISO 42001/NIST AI RMF) met LLM-evals en AI-advisor; relevant als AI-governance-aanvulling, niet als algemeen ISMS, en let op de licentie.
- **gigachad-grc** — https://github.com/grcengineering/gigachad-grc — **Elastic License 2.0 (niet-OSI, geen managed-service-resale)**; microservices + Swagger + MCP-server + AI-risk-scoring.
- **gapps** — https://github.com/bmarsh9/gapps — **AGPL-3.0 + Commons Clause (source-available, geen resale)**; REST-API, Docker, geen AI.
- **strongdm/comply** — https://github.com/strongdm/comply — Apache-2.0, volledig OSS, **maar effectief verlaten** (laatste release nov 2021); SOC2-markdown→PDF-pipeline, CLI-only.
- **⚠️ Verlaten — GovReady-Q** — https://github.com/GovReady/govready-q — NIST/FedRAMP-GRC, laatste commit dec 2024; niet meer aanraden.
- **⚠️ Licentie-val algemeen:** "open source"-branding is in deze categorie onbetrouwbaar — Eramba (closed), OpenGRC (CC-NC), VerifyWise (BSL), gigachad (ELv2) en gapps (Commons Clause) zijn allemaal *restricted*, niet OSI-open. Verifieer altijd de licentie in de repo.

---

## 2. Policy-as-code (machine-afdwingbaar beleid)

Technische GOVERN-laag: declaratieve regels die infra/clusters/apps toetsen aan beleid. Volwassen,
breed gedragen, vrijwel allemaal Apache-2.0 (permissief) en zelf-hostbaar zonder SaaS-afhankelijkheid.

### 2.1 Open Policy Agent (OPA)

1. **Naam + URL:** Open Policy Agent — https://github.com/open-policy-agent/opa
2. **CSF-functie(s):** GOVERN (beleidsafdwinging), PROTECT (toegang/configuratie-handhaving).
3. **Capability:** Policy-as-code / general-purpose policy engine met de Rego-taal.
4. **Omschrijving:** CNCF-graduated, domein-agnostische policy-engine: één manier om beleid uit te drukken en af te dwingen over Kubernetes, CI/CD, microservices, API-gateways en data. Companion **Gatekeeper** levert de K8s-admission-controller.
5. **Rijpheid:** **HOOG.** v1.17.1 (8 juni 2026), ~11.9k sterren, ~2–3 commits/dag, CNCF graduated (2021). Maandelijkse minors.
6. **Licentie:** **Apache-2.0** (permissief, geen copyleft). Kern niet open-core-gegated; Styra is commercieel sponsor maar gate't geen kernfunctionaliteit.
7. **EU-soevereiniteit:** **STERK.** Sidecar/daemon/embedded Go-library/Wasm; volledig zelf-hostbaar, geen SaaS, geen data-uitvoer.
8. **Integreerbaarheid:** **CLI + REST API + library + Wasm.** `opa` CLI, REST (`/v1/data/...`), Go SDK; uitstekend koppelbaar aan een AI-dirigent.
9. **AI-native koppelbaarheid:** **DEELS.** Geen *officiële* MCP-server (door maintainer bevestigd, juni 2025). Wel een third-party **OPA MCP (Orygn LLC, MIT)** in de officiële OPA-ecosystem-lijst (niche, ~3 sterren). Schone REST-API + JSON maakt het anderszins agent-vriendelijk.
10. **Stack/taal:** Go; policy-taal Rego. Runtime: native binary / container / Wasm.
11. **Fit-score:** **5/5** — rijp, permissief, EU-soeverein zelf-hostbaar, breed integreerbaar; alleen de MCP-laag is nog niet officieel.
12. **Bronnen:** https://github.com/open-policy-agent/opa · https://www.cncf.io/projects/open-policy-agent-opa/ · https://github.com/open-policy-agent/opa/discussions/697

### 2.2 Kyverno

1. **Naam + URL:** Kyverno — https://github.com/kyverno/kyverno
2. **CSF-functie(s):** GOVERN (beleid), PROTECT (handhaving in Kubernetes).
3. **Capability:** Policy-as-code, Kubernetes-native (YAML, geen nieuwe DSL).
4. **Omschrijving:** CNCF-graduated K8s admission-controller die beleid in pure YAML valideert/muteert/genereert; ingezet bij o.a. Deutsche Telekom, Vodafone, Bloomberg, Spotify.
5. **Rijpheid:** **HOOG.** v1.18.1 (18 mei 2026), ~9k sterren, **CNCF graduated (24 maart 2026)**. Nieuwe minor ~elk kwartaal.
6. **Licentie:** **Apache-2.0** (kern). **Open-core caveat:** Nirmata verkoopt "N4K"-enterprise-distributie eromheen, maar gate't geen kernfunctionaliteit.
7. **EU-soevereiniteit:** **STERK.** Draait in je eigen cluster; geen SaaS.
8. **Integreerbaarheid:** **CLI + K8s-API.** `kyverno apply`/`kyverno test`; werkt via admission-webhooks. Lagere drempel dan Rego door pure YAML.
9. **AI-native koppelbaarheid:** **DEELS.** **nirmata/kyverno-mcp** MCP-server (AGPL-3.0, ~19 sterren, jan 2026; werkt met Claude Desktop/Cursor/Amazon Q) — let op: vendor-onderhouden, niet upstream, en AGPL i.p.v. de Apache-2.0-kern.
10. **Stack/taal:** Go; beleid in YAML. Runtime: Kubernetes.
11. **Fit-score:** **4/5** — rijp, permissieve kern, EU-soeverein; afgewaardeerd t.o.v. OPA omdat het scope-beperkt is tot Kubernetes (geen general-purpose engine).
12. **Bronnen:** https://github.com/kyverno/kyverno · https://www.cncf.io/announcements/2026/03/24/ (CNCF graduation) · https://github.com/nirmata/kyverno-mcp

### 2.3 Cedar (AWS) — *sterkste AI-native verhaal van de set*

1. **Naam + URL:** Cedar — https://github.com/cedar-policy/cedar
2. **CSF-functie(s):** GOVERN (autorisatiebeleid), PROTECT (toegangsbeheer/ABAC).
3. **Capability:** Policy-as-code op applicatie-/agentniveau (authorization, ABAC) — onderscheidt zich van de IaC-scanners hierboven.
4. **Omschrijving:** Verifieerbare (SMT/Lean-gevalideerde) policy-taal en -engine voor fijnmazige autorisatie; toepasbaar als CLI, Rust-crate of Wasm in apps en agent-workflows.
5. **Rijpheid:** **HOOG.** v4.11.1 (9 juni 2026), ~1.55k sterren, 73 releases, OpenSSF Best-Practices-badge. Cadans ~4–8 weken.
6. **Licentie:** **Apache-2.0** doorheen het hele project (permissief, geen open-core-gating).
7. **EU-soevereiniteit:** **STERK.** Lokale CLI / crate / Wasm; geen cloud-afhankelijkheid. (Let op: hoewel door AWS opgezet, draait Cedar zelf volledig lokaal/embedded — géén SaaS-vereiste.)
8. **Integreerbaarheid:** **CLI + library + Wasm.** `cedar-policy-cli`, Rust-crate-API, `cedar-wasm` voor JS/TS.
9. **AI-native koppelbaarheid:** **JA (sterkst).** Officiële **cedar-for-agents** met **cedar-analysis-mcp-server** + MCP-tools-SDK; gebruikt als autorisatie-engine in Amazon Bedrock AgentCore (MCP-tool-filtering, NL→Cedar-vertaling met SMT-validatie). Microsofts Agent Governance Toolkit behandelt Cedar als first-class beleidstaal.
10. **Stack/taal:** Rust; eigen Cedar-policy-taal. Runtime: native/Wasm/embedded.
11. **Fit-score:** **5/5** — rijp, permissief, EU-soeverein-embeddable en de meest agent/MCP-native optie; ideaal voor het governen van AI-agent-autorisatie zelf.
12. **Bronnen:** https://github.com/cedar-policy/cedar · https://github.com/cedar-policy/cedar-for-agents · https://github.com/microsoft/agent-governance-toolkit

### Long tail — policy-as-code

- **Conftest** — https://github.com/open-policy-agent/conftest — Apache-2.0; CLI die OPA/Rego op config-bestanden draait in CI/CD (v0.68.2, apr 2026); geen REST-API.
- **Checkov** — https://github.com/bridgecrewio/checkov — Apache-2.0; 1.000+ ingebouwde IaC-policies (Terraform/K8s/CloudFormation/…), zeer actief (meerdere releases/week), CLI/library met SARIF/JSON-output; geen officiële MCP.
- **Trivy** — https://github.com/aquasecurity/trivy — Apache-2.0; ~35k sterren, multi-layer scanning incl. IaC-misconfig (overlapt Checkov's IaC-rol).
- **Cloud Custodian** — https://github.com/cloud-custodian/cloud-custodian — CNCF-incubating multi-cloud governance-DSL.
- **Kubernetes ValidatingAdmissionPolicy (CEL)** — ingebouwd in K8s (GA sinds v1.30); native lichtgewicht alternatief voor OPA/Kyverno.
- **⚠️ Vermijden — Regula/Fugue** — https://github.com/fugue/regula — **gearchiveerd sept 2024** (Snyk-overname; code → snyk/policy-engine, dunne community-tractie).
- **⚠️ Vermijden — Datree** — https://github.com/datreeio/datree — **gearchiveerd juni 2024, bedrijf opgeheven** (was open-core; SaaS-backend permanent offline).
- **⚠️ Niet-OSS — HashiCorp Sentinel** — proprietary, alleen binnen HCP/Terraform; niet zelf-hostbaar als standalone.

---

## 3. Beleidsbeheer — lifecycle van geschreven beleidsdocumenten

Het beheren van *geschreven* security-policies (draft → review → approve → publish → her-review),
met framework-koppeling en eigenaarschap. **Kernbevinding: er is geen toegewijde OSS-tool** die dit
doet zoals commerciële producten (PolicyHub, NAVEX PolicyTech). De beste dekking komt van de
GRC-platforms uit §1; daarnaast configureerbare DMS'en en een OSCAL-route.

### 3.1 CISO Assistant — beleidsmodule (zie §1.1 voor volledige scorekaart)

Beste lifecycle-match: native markdown-editor, states **Draft → Review → Approved → Retired**,
approval-workflows met sign-off, directe koppeling van policies aan controls/frameworks, export naar
nette documenten. Module is relatief nieuw (v3.14, maart 2026) — diepte van versionering/diff-historie
nog niet volledig publiek gedocumenteerd. Licentie/EU/integratie identiek aan §1.1 (AGPL-3.0,
zelf-hostbaar, API-first). **Fit voor beleidsbeheer specifiek: 4/5** (module jong, maar enige OSS-optie
met echte lifecycle + framework-mapping + actieve ontwikkeling).
**Bron:** https://intuitem.com/whats-new-ciso-assistant-2026-w11/

### 3.2 Eramba — beleidsmodule (zie §1.3 voor volledige scorekaart + licentie-voorbehoud)

Functioneel de volwassenste review-discipline: approval-workflow, **automatische review-records per
deadline** (periodieke her-review afgedwongen), versie/reviewer/audit-trail, publieke policy-portal voor
distributie. **Maar:** de licentie is betwist (geen officiële broncode → niet aantoonbaar OSI-open),
waardoor Eramba onder de harde open-source-poort van deze blueprint afvalt ondanks de sterke
beleidsfunctionaliteit. **Fit voor beleidsbeheer specifiek: 2/5 (licentie-diskwalificatie).**
**Bron:** https://www.eramba.org/learning/courses/35

### 3.3 Mayan EDMS — *generieke DMS, configureerbaar tot beleids-lifecycle*

1. **Naam + URL:** Mayan EDMS — https://gitlab.com/mayan-edms/mayan-edms (mirror: https://github.com/mayan-edms/mayan-edms)
2. **CSF-functie(s):** GOVERN (beleidsdocument-lifecycle, generiek).
3. **Capability:** Document-lifecycle/-management; in te richten als policy-workflow.
4. **Omschrijving:** Volwaardig open-source DMS met workflow-engine (multi-step approval), versiebeheer met revert, RBAC per document/versie, retentie en audit-trail. Niet security-specifiek — vereist configuratie om draft/review/approve-states voor policies te modelleren.
5. **Rijpheid:** **MIDDEN-HOOG.** Actief onderhouden, volwassen featureset; geen security-/framework-templates out-of-the-box.
6. **Licentie:** **Apache-2.0** (permissief).
7. **EU-soevereiniteit:** **STERK.** Zelf-hostbaar (Docker), geen SaaS-vereiste.
8. **Integreerbaarheid:** **REST API + CLI.** Goed scriptbaar; koppelbaar aan een AI-dirigent.
9. **AI-native koppelbaarheid:** **NEE** (geen MCP/LLM-features; wel schone REST-API als basis).
10. **Stack/taal:** Python/Django; PostgreSQL; Docker.
11. **Fit-score:** **3/5** — rijp, permissief en EU-soeverein, maar **één serieus bezwaar**: geen security-/framework-context out-of-the-box; vergt significante inrichting om policy-lifecycle te modelleren.
12. **Bronnen:** https://docs.mayan-edms.com/chapters/features.html · https://gitlab.com/mayan-edms/mayan-edms

### Long tail — beleidsbeheer

- **IBM Compliance Trestle** — https://github.com/IBM/compliance-trestle — Apache-2.0, actief (v4.0.3, mei 2026); beheert compliance-docs in NIST **OSCAL** (machine-leesbaar) in Git met PR-review — "policy-as-code"-route voor OSCAL-omgevingen, niet voor leesbare Word/PDF-policies.
- **Comply (strongdm)** — https://github.com/strongdm/comply — Apache-2.0; markdown→PDF policy-pipeline met SOC2-templates en ticketing — **maar feitelijk verlaten** (laatste release v1.6.0, nov 2021), geen formele lifecycle-states.
- **Hack23/ISMS-PUBLIC** — https://github.com/Hack23/ISMS-PUBLIC — 38 publieke ISO 27001-gealigneerde policy-documenten in Markdown; uitstekende *startsjablonen*, geen tooling.
- **0xdefendA/policies** — https://github.com/0xdefendA/policies — MPL-2.0 policy-templates; inactief, geen workflow.
- **Outline / BookStack** — https://github.com/outline/outline · https://github.com/BookStackApp/BookStack — open-source, zelf-hostbare wiki's waarin policies (en RASCI-tabellen) handmatig als gestructureerde markdown worden bijgehouden; geen managed lifecycle.

---

## 4. Governance-rollen & verantwoordelijkheidstoewijzing (RASCI)

**Kernbevinding: dit is een bevestigde gap in open source.** Toegewijde RACI/RASCI-tooling is óf
commercieel (LucidChart, Smartsheet, Miro), óf bestaat als hobby-/POC-repo's met 1–5 sterren en
onduidelijk onderhoud. De GRC-platforms uit §1 bieden hooguit *eigenaarschap-velden* (owner per control/risk),
geen volledige R/A/C/I-decompositie. De pragmatische OSS-route is een GRC-tool (eigenaarschap) +
een wiki (RASCI-matrix als document). **Geen tool haalt hier een volledige scorekaart-fit van ≥3.**

### 4.1 CISO Assistant / Eramba — partiële dekking via eigenaarschap

Beide (zie §1.1/§1.2) bieden RBAC en owner/manager-toewijzing per GRC-object (risk, control, policy),
maar **geen native RACI-matrix** — eigenaarschap is een enkel veld, niet de volledige R/A/C/I-uitsplitsing.
Dit is de "best beschikbare" OSS-benadering voor verantwoordelijkheidsgovernance, niet een echte RASCI-tool.
**Fit voor RASCI specifiek: 2/5** (bestaat en bruikbaar als owner-register, maar dekt de capability niet volledig).
**Bronnen:** https://github.com/intuitem/ciso-assistant-community · https://www.eramba.org/get-community

### Long tail — RASCI (allen laag-volwassen / niet productieklaar)

- **joelparkerhenderson/responsibility-assignment-matrix** — https://github.com/joelparkerhenderson/responsibility-assignment-matrix — referentie-/documentatierepo (RACI/RASCI/DACI/RAPID), géén applicatie, maar nuttig als conceptbron.
- **microsoft/Azure-RACI-Toolkit** — https://github.com/microsoft/Azure-RACI-Toolkit — MIT; Excel/Word-governance-RACI-template (Azure-context, maar de structuur is breder bruikbaar als sjabloon).
- **ProcessAce** — https://github.com/topics/raci — AI-gedreven proces-/RACI-documentatie (Node.js, juni 2026, ~5 sterren); proces-discovery, geen governance-register.
- **Firesphere/rasci-tables** — https://github.com/Firesphere/rasci-tables — PHP/SilverStripe RASCI-webapp met ISO 27001-tag; ~2 sterren, feitelijk persoonlijk project.
- **selcuksert/raci-app** / **alfredang/raci** — kleine RACI-webapps (Spring Boot resp. vanilla-JS/Firebase); te licht / ogen verlaten.

---

## 5. Bestuurlijke rapportage & KPI-/risk-dashboards

Het zichtbaar maken van security-posture aan bestuur: KPI's, risk-scores, compliance-posture,
executive-rapportage. De OSS-ruimte splitst in (a) GRC-rapportage (CISO Assistant), (b) operationele
posture-/compliance-dashboards (Wazuh, Prowler, DefectDojo), en (c) een generieke visualisatielaag
(Grafana). Echte "executive CISO-KPI-dashboards" als kant-en-klare OSS bestaan vrijwel niet — wel
posture-feeds die je via Grafana naar bestuurlijke views kunt tillen.

### 5.1 Wazuh — *compliance-posture-dashboards*

1. **Naam + URL:** Wazuh — https://github.com/wazuh/wazuh
2. **CSF-functie(s):** GOVERN (compliance-rapportage), DETECT/RESPOND (SIEM/XDR-kern).
3. **Capability:** Doorlopende compliance-monitoring met ingebouwde dashboards + auditrapporten.
4. **Omschrijving:** Open-source SIEM/XDR met ingebouwde compliance-dashboards (PCI DSS v4.0, GDPR, HIPAA, NIST 800-53, TSC), SCA-scans met posture-scoring en PDF/HTML-auditrapporten.
5. **Rijpheid:** **HOOG.** v4.14.5 (apr 2026), ~15.9k sterren; brede deploymentopties (Docker/K8s/Ansible).
6. **Licentie:** **GPL-2.0** (copyleft).
7. **EU-soevereiniteit:** **STERK.** Volledig zelf-hostbaar, geen SaaS-vereiste.
8. **Integreerbaarheid:** **REST API + UI.** Gedocumenteerde API; data te exporteren/feeden naar BI/Grafana.
9. **AI-native koppelbaarheid:** **NEE** (geen MCP/LLM-features in de open-source editie).
10. **Stack/taal:** C/C++ (engine), met OpenSearch/dashboards-laag.
11. **Fit-score:** **4/5** — rijp, EU-soeverein, sterke compliance-posture-views; afgewaardeerd omdat het geen *bestuurlijke* KPI-laag is (operationeel/compliance-georiënteerd) en geen AI-haakjes heeft.
12. **Bronnen:** https://github.com/wazuh/wazuh · https://wazuh.com/resources/use-cases/regulatory-compliance/

### 5.2 Prowler — *cloud-posture (CSPM) met MCP*

1. **Naam + URL:** Prowler — https://github.com/prowler-cloud/prowler
2. **CSF-functie(s):** GOVERN (compliance-mapping/-rapportage), IDENTIFY (posture-assessment).
3. **Capability:** Cloud Security Posture Management met compliance-dashboards en frameworkmapping.
4. **Omschrijving:** Multi-cloud (AWS/Azure/GCP/K8s/GitHub/M365) posture-scanner met mappings naar NIST CSF, NIST 800-53, CIS, NIS2, GDPR, PCI-DSS, SOC2; export naar JSON/CSV/HTML.
5. **Rijpheid:** **HOOG.** v5.30.2 (17 juni 2026), ~14k sterren, zeer actief.
6. **Licentie:** **Apache-2.0** (permissief). **Open-core caveat:** de commerciële "Prowler App" levert een rijkere dashboard-UI; de OSS-CLI/API is krachtig maar het dashboard is basaler zonder de app-laag.
7. **EU-soevereiniteit:** **STERK.** Zelf-hostbaar (Docker, volledige stack); scant je eigen cloud-accounts.
8. **Integreerbaarheid:** **CLI + REST API.** Django-REST-API (`/api/v1/docs`).
9. **AI-native koppelbaarheid:** **JA.** "Lighthouse" AI-assistent op basis van een **MCP-server** (beschikbaar als MCP-tool); schone gestructureerde output. Sterkste AI-native dashboard-optie in deze categorie.
10. **Stack/taal:** Python; Docker.
11. **Fit-score:** **4/5** — rijp, permissief, EU-soeverein zelf-hostbaar én MCP-native; afgewaardeerd omdat het rijkere dashboard achter de commerciële app zit en de scope cloud-posture is (niet bestuurlijke KPI breed).
12. **Bronnen:** https://github.com/prowler-cloud/prowler · https://prowler.com/use-cases/cloud-security-posture-management

### 5.3 DefectDojo — *AppSec/DevSecOps-KPI's*

1. **Naam + URL:** DefectDojo — https://github.com/DefectDojo/django-DefectDojo
2. **CSF-functie(s):** GOVERN (security-metrics/KPI-rapportage), IDENTIFY (vuln-management).
3. **Capability:** Vulnerability-management-pijplijn met KPI-dashboards (MTTR, SLA, open/closed findings).
4. **Omschrijving:** OWASP-flagship ASPM-platform: dashboard-tiles, trend-metrics, SLA-/MTTR-tracking, deduplicatie en engagement-counters over de hele AppSec-pijplijn.
5. **Rijpheid:** **HOOG.** v3.0.0 (15 juni 2026), ~4.8k sterren, OWASP-flagship.
6. **Licentie:** **BSD-3-Clause** (permissief). **Open-core caveat:** Pro-editie voegt auto-enrichment/prioritering toe; KPI-dashboards zitten in de open-source editie.
7. **EU-soevereiniteit:** **STERK.** Zelf-hostbaar (Docker Compose/Kubernetes).
8. **Integreerbaarheid:** **REST API v2 + CLI-wrappers.** Sterk geautomatiseerd; JIRA-integratie.
9. **AI-native koppelbaarheid:** **NEE** in de open-source editie (geen MCP; AI-enrichment zit in Pro).
10. **Stack/taal:** Python/Django; Docker/K8s.
11. **Fit-score:** **4/5** — rijp, permissief, EU-soeverein met sterke KPI-/SLA-/MTTR-metrics; afgewaardeerd omdat de scope AppSec/vuln is (geen brede bestuurlijke risk-KPI) en er geen AI-haakjes in de OSS-editie zitten.
12. **Bronnen:** https://github.com/DefectDojo/django-DefectDojo · https://owasp.org/www-project-defectdojo/ · https://docs.defectdojo.com/metrics_reports/dashboards/introduction_dashboard/

### Long tail — dashboards/rapportage

- **Grafana** — https://github.com/grafana/grafana — AGPL-3.0 (core); dé visualisatielaag voor security-KPI's, maar **geen security-tool zelf** — vereist een databron (Wazuh/Prowler/…). Community-templates bestaan (ISO 27001-audit, Azure-compliance via CloudQuery, Docker-CIS via Sysdig), maar geen gezaghebbend OSS-CISO-KPI-template.
- **Faraday** — https://github.com/infobyte/faraday — GPL-3.0; aggregeert vuln-data over 80+ tools met management-views; meer security-ops dan bestuurlijke KPI.
- **CISO Assistant** (zie §1.1) — levert tevens de GRC-/risk-/compliance-rapportagelaag; voor *bestuurlijke* risk-KPI's de meest geschikte OSS-GRC-bron om naar Grafana te feeden.
- **⚠️ POC-only — SiteQ8/CISO-Dashboard** (https://github.com/SiteQ8/CISO-Dashboard, MIT, ~3 sterren) en **abdmath/Security-Risk-Assessment-Dashboard** (~1 ster) — executive-KPI-/NIST-CSF-mapping-startertemplates, niet productieklaar.

---

## Niet-gedekt / gaps (voedt de gap-analyse)

1. **RASCI / verantwoordelijkheidstoewijzing — grootste gap.** Geen enkele volwassen, zelf-hostbare
   open-source tool voor R/A/C/I-governance van security-rollen. GRC-platforms bieden slechts
   enkelvoudige eigenaarschap-velden, geen volledige decompositie. De praktische OSS-route is een
   handmatige wiki-/markdown-matrix (Outline/BookStack/Obsidian) gekoppeld aan GRC-control-eigenaarschap —
   met volledig handmatige actualisatie- en staleness-bewaking. **Kandidaat-bouwtaak voor cisochat:**
   een lichte RASCI-laag bovenop de GRC-API (CISO Assistant) zou een echt gat vullen.

2. **Bestuurlijke (executive) security-KPI-dashboards — gat in kant-en-klare OSS.** Wel posture-/
   compliance-dashboards (Wazuh, Prowler, DefectDojo) en GRC-rapportage (CISO Assistant), maar géén
   volwassen open-source "CISO-board-view" out-of-the-box. De realistische route is GRC-data + Grafana,
   wat eigen dashboard-engineering vergt; de bestaande "CISO-dashboard"-repo's zijn POC's (1–3 sterren).

3. **Beleids-lifecycle (geschreven policies) — geen toegewijde OSS-tool.** Geen open-source equivalent
   van PolicyHub/PolicyTech voor pure beleidsdocument-lifecycle inclusief *medewerker-acknowledgement-
   tracking* en *geautomatiseerde her-review-escalatie*. CISO Assistant (jonge module) en Eramba
   (review-records, maar dunne community-API) komen het dichtst; acknowledgement-tracking ontbreekt OSS-breed.

4. **Officiële MCP-/AI-native governance-laag — opkomend, maar nog onrijp aan de top.** Het beeld is
   beter dan een jaar geleden: **Probo** (MIT, MCP-server met 270+ tools) en **unidoc/isms** (Apache-2.0,
   MCP met 22 tools) leveren een MCP-native GRC-koppelvlak, en aan de policy-as-code-kant hebben **Cedar**
   (agent-autorisatie) en **Prowler** (Lighthouse) een first-class MCP-haak. **Maar:** de rijpste GRC-tool
   (CISO Assistant) heeft nog géén MCP-server (koppeling via REST), en de wél MCP-native GRC-opties zijn
   jonger/kleiner (Probo) of pril (unidoc/isms). OPA/Kyverno leunen op third-party/vendor-MCP's (resp.
   niche en AGPL). **Conclusie: een rijpe én MCP-native GRC-governancelaag bestaat nog niet in één tool —
   de keuze is "rijp zonder MCP" (CISO Assistant + eigen API-koppeling) óf "MCP-native maar jonger" (Probo).**

5. **OSCAL-route is technisch, niet bestuurlijk.** IBM Compliance Trestle dekt machine-leesbare
   compliance-documentatie sterk, maar levert geen leesbare beleidsdocumenten of bestuurlijke views —
   een brug tussen OSCAL en human-readable governance ontbreekt in volwassen OSS.

---

### Open punten / twijfels bij de brief

- **Eramba-licentie (belangrijk voorbehoud):** twee onderzoekslijnen spraken elkaar tegen. De officiële
  Eramba-org publiceert **geen broncode-repo** (alleen Docker-helpers); het enige GPLv2-bewijs staat in een
  oude *onofficiële* mirror (`sys02/eramba`, 1 ster), niet in de levende codebase. Daarom is Eramba hier
  als **niet aantoonbaar OSI-open source** behandeld (fit-score 2/5) en afgewaardeerd onder de harde poort —
  ondanks sterke beleidsfunctionaliteit. Wil je Eramba toch overwegen, verifieer dan eerst zelf de
  feitelijke licentie van de broncode die je deployt.
- **Scope-overlap met andere CSF-functies:** veel sterke "GOVERN"-tools (Wazuh, Prowler, DefectDojo)
  zijn primair DETECT/IDENTIFY-tools die *compliance-rapportage* leveren. Ze zijn hier opgenomen vanwege
  hun GOVERN-rapportagewaarde, maar horen inhoudelijk ook in andere functie-documenten — let op
  dubbeltelling bij de uiteindelijke blueprint.
- **CISO Assistant beleidsmodule** is jong (maart 2026); diepte van versionering/diff-historie is nog
  niet publiek geverifieerd — bij selectie een eigen hands-on-check aanbevolen.
