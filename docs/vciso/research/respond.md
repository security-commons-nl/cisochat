# RESPOND — open-source tooling landscape (NIST CSF 2.0)

> **Scope.** Dit document inventariseert open-source tooling voor de NIST CSF 2.0-functie **RESPOND** (RS)
> ten behoeve van een generieke, framework-agnostische vCISO-blueprint. De functie RESPOND omvat
> incident management & case management (RS.MA), incident-analyse (RS.AN), incident-respons rapportage &
> communicatie (RS.CO), incident-mitigatie (RS.MI) en — in samenhang met RECOVER — de aanloop naar
> verbeteringen. Per sub-categorie zijn de **top 2–3 tools** volledig uitgewerkt (12-velden scorekaart);
> overige vondsten staan als *long tail* (naam + URL + 1 zin).
> Harde poort: **alléén open source** — open-core wordt beoordeeld op uitsluitend de community-editie,
> met expliciete vermelding van wat achter de betaalmuur zit. Licentie-vallen (proprietary "community"-
> tiers, BSL/SSPL/PolyForm/Commons Clause/source-available) worden expliciet benoemd; OSI-goedkeuring
> is de norm. EU-soevereiniteit is een zachte weging (zelf-hostbaarheid + dataresidentie).
> Alle tool-claims zijn voorzien van ≥1 bron-URL. Peildatum onderzoek: **juni 2026**.

> ⚠️ **Belangrijkste licentie-bevinding (poort-relevant).** **TheHive 5 is GEEN open source meer.** Sinds
> v5 (2022) hanteert StrangeBee een proprietary, tiered commercieel model (Community / Gold / Platinum).
> De "Community"-editie is een *gratis proprietary licentie* met gebruiksrestricties (geen productie/
> educatie-test), geen gepubliceerde broncode, en degradeert naar read-only zonder licentiesleutel. De
> laatste AGPL-versies (TheHive 3 & 4) zijn in augustus 2025 end-of-public-availability verklaard en de
> originele GitHub-repo is 5 december 2025 gearchiveerd (read-only). **TheHive 5 valt daarmee buiten de
> harde poort.** De facto open-source opvolger voor case management is **DFIR-IRIS** (LGPL-3.0).
> **Cortex** (het analyse-engine zusterproject) is daarentegen AGPL-3.0 gebleven en blijft open source.

---

## 1. Incident response & case management

Het open-source landschap voor IR-case-management is in 2024–2026 grondig herschikt door de commerciële
pivot van TheHive. De duidelijke open-source winnaar is nu **DFIR-IRIS** (LGPL-3.0, actief). **Cortex**
blijft als observable-analyse-engine relevant (AGPL-3.0). TheHive 5 is uitgesloten (proprietary). In de
brede DFIR-laag vult **Velociraptor** (endpoint-respons/hunt) de technische kant van RS.AN/RS.MI.

### 1.1 DFIR-IRIS — *primaire aanbeveling RESPOND / case management*

1. **Naam + URL:** DFIR-IRIS (iris-web) — https://github.com/dfir-iris/iris-web
2. **CSF-functie(s):** RESPOND (primair: RS.MA incident management, RS.AN analyse, RS.CO rapportage/communicatie). Raakt RECOVER via case-documentatie.
3. **Capability:** Collaboratief incident-respons- en case-managementplatform: cases, IoC's, notes, taken, evidence en tijdlijnen.
4. **Omschrijving:** Gebouwd "voor hoe IR werkelijk werkt" — multi-analist samenwerking aan cases met
   gedeelde IoC-registratie, evidence-tracking en tijdlijnen. Modulair plugin-systeem; case-template-
   bibliotheek voor veelvoorkomende incidenttypes (community-template-set gepubliceerd maart 2026). Breed
   omarmd als de open-source opvolger nu TheHive's community-editie commercieel/stilstaand werd.
5. **Rijpheid:** **Hoog.** Stabiele release v2.4.27 (27 januari 2026); v2.5.0-beta in ontwikkeling. Actieve
   module-updates begin 2026 (o.a. iris-webhooks-module 27 jan 2026). Community-gefinancierd via Open Collective.
6. **Licentie:** **LGPL-3.0-only** (OSI-goedgekeurd, zwak copyleft). **Volledig open source** — geen
   commerciële tiers, geen licentiesleutels, geen betaalmuur. Geen open-core constructie.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar (Docker Compose, on-prem of eigen cloud). Geen verplichte
   SaaS-component. Dataresidentie 100% in eigen beheer. Sterke fit voor EU/overheid.
8. **Integreerbaarheid:** Volledige REST API. Module-/plugin-systeem. Integraties met MISP, VirusTotal,
   IntelOwl, WebHooks; gedocumenteerde Wazuh-koppeling.
9. **AI-native koppelbaarheid:** Deels. Geen native MCP-server (juni 2026), maar volledige REST API +
   gestructureerde JSON maken LLM-pipelines (triage, samenvatting, IoC-verrijking) goed bouwbaar.
10. **Stack/taal:** Python (Flask backend), PostgreSQL. Docker Compose-deployment.
11. **Fit-score: 5/5.** Enige werkelijk open-source, actief onderhouden IR-case-managementplatform van
    productiekwaliteit; zelf-hostbaar; permissief-genoeg copyleft; sterke EU-fit. Eerste keuze voor de blueprint.
12. **Bronnen:**
    - https://github.com/dfir-iris/iris-web (release v2.4.27, 27 jan 2026; LGPL-3.0 badge geverifieerd)
    - https://www.dfir-iris.org/ · https://docs.dfir-iris.org/latest/
    - https://opencollective.com/dfir-iris
    - https://www.msspalert.com/native/5-open-source-incident-response-tools-for-mssps

---

### 1.2 Cortex — *aanbeveling voor observable-analyse / active response*

1. **Naam + URL:** Cortex — https://github.com/TheHive-Project/Cortex (analyzers: https://github.com/TheHive-Project/Cortex-Analyzers)
2. **CSF-functie(s):** RESPOND (RS.AN incident-analyse, RS.MI active response). Raakt DETECT (observable-verrijking).
3. **Capability:** Observable Analysis & Active Response Engine: analyseert IP's, domeinen, URL's, hashes,
   e-mailadressen via pluggable analyzers/responders.
4. **Omschrijving:** Schaalbare engine die observables één-voor-één of in bulk verrijkt en active-response-
   acties uitvoert via Python "workers" (analyzers + responders). Historisch het analyse-zusterproject van
   TheHive, maar werkt onafhankelijk en koppelt ook aan andere platforms (o.a. DFIR-IRIS, MISP).
5. **Rijpheid:** **Middel.** Functioneel volwassen, maar het ontwikkeltempo is gezakt: core laatst bijgewerkt
   ~16 juli 2025; Cortex-Analyzers 3.3.8 (21 maart 2025). Stabiel, maar minder actief dan voorheen — let op
   onderhouds-/houdbaarheidsrisico.
6. **Licentie:** **AGPL-3.0-only** (OSI-goedgekeurd, sterk netwerk-copyleft). **Volledig open source** —
   geen tiers/licentiesleutel (in tegenstelling tot TheHive 5). Geverifieerd in repo-LICENSE-bestand.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar (Docker, on-prem). Geen SaaS-verplichting. Let op: veel
   analyzers roepen externe (deels non-EU) API's aan — dataminimalisatie per analyzer beoordelen.
8. **Integreerbaarheid:** Volledige stateless REST API (horizontaal schaalbaar). Python-client `Cortex4py`.
   Analyzers in Python (uitbreidbaar naar elke taal).
9. **AI-native koppelbaarheid:** Deels. REST API + pluggable analyzers laten LLM-analyzers/responders toe;
   geen native AI-features of MCP.
10. **Stack/taal:** Scala (Play/Akka backend), Elasticsearch. Analyzers in Python.
11. **Fit-score: 3/5.** Sterke, echt-open-source verrijkings-/responsmotor met AGPL-garantie, maar dalend
    ontwikkeltempo en Elasticsearch-/Scala-zwaarte drukken de fit. Optionele aanvulling, geen kern.
12. **Bronnen:**
    - https://github.com/TheHive-Project/Cortex · https://github.com/TheHive-Project/Cortex/blob/master/LICENSE (AGPL-3.0 geverifieerd)
    - https://strangebee.com/blog/cortex-analyzers-3-3-8-release-new-tools-fresh-upgrades-and-more/
    - https://github.com/TheHive-Project/Cortex4py

---

### 1.3 Velociraptor — *aanbeveling voor endpoint-respons & live-collectie (RS.AN/RS.MI)*

1. **Naam + URL:** Velociraptor — https://github.com/Velocidex/velociraptor · https://docs.velociraptor.app/
2. **CSF-functie(s):** RESPOND (RS.AN analyse, RS.MI mitigatie/containment via live response). Raakt DETECT (hunting).
3. **Capability:** Endpoint-monitoring, digital forensics en cyber-response: fleet-wide artifact-collectie,
   threat hunting en live response via VQL (Velociraptor Query Language).
4. **Omschrijving:** Krachtig DFIR-platform dat over de hele endpoint-vloot artifacts verzamelt, hunts
   uitvoert en live-response/containment ondersteunt. Schaalt naar 10–15k endpoints op één server (100k+
   multi-frontend). Actief onderhouden artifact-bibliotheek. Ontwikkeld door DFIR-professionals, nu door Rapid7.
5. **Rijpheid:** **Hoog.** Brede adoptie, CISA-erkend, actieve community-artifact-library. Productie-rijp.
6. **Licentie:** AGPL-3.0 (open source). Rapid7 biedt een commercieel ondersteunde variant *bovenop* de
   open-source kern; de kern zelf kent geen per-seat-restricties. ⚠️ Verifieer de exacte SPDX in het
   repo-LICENSE-bestand vóór gebruik (AGPL bevestigd in meerdere bronnen, niet in dit onderzoek 1-op-1 uit het LICENSE-bestand gelezen).
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar; volledige controle bij de operator; geen verplichte cloud.
8. **Integreerbaarheid:** API/gRPC, krachtige VQL-querytaal, CLI. Goede automatiseerbaarheid.
9. **AI-native koppelbaarheid:** Deels. API + VQL-output zijn goed te voeden aan LLM-analyse; geen native MCP.
10. **Stack/taal:** Go (server + client), VQL als query-laag.
11. **Fit-score: 4/5.** Beste open-source endpoint-respons/hunt-tool; dekt de technische RS.AN/RS.MI-kant die
    case-management (DFIR-IRIS) niet doet. Complementair, geen overlap. (Multi-functie: ook DETECT.)
12. **Bronnen:**
    - https://docs.velociraptor.app/ · https://www.rapid7.com/products/velociraptor/
    - https://www.cisa.gov/resources-tools/services/velociraptor

> **Multi-functie / dedup-noot.** Velociraptor, Timesketch, GRR, OpenRelik en Plaso zijn primair DFIR-tools
> die zowel **DETECT** als **RESPOND** raken. Werk ze niet dubbel uit in beide functie-documenten; hoofd-
> uitwerking in één functie, kruisverwijzing in de andere. DFIR-IRIS is primair RESPOND. Cortex raakt DETECT.

**Long tail — case management & DFIR-collectie:**
- **TheHive 5** — https://github.com/StrangeBeeCorp (feedback) — ⛔ **UITGESLOTEN: proprietary** (Community-tier = gratis, niet OSS); AGPL-era v4 gearchiveerd aug/dec 2025.
- **Kanvas** — https://www.helpnetsecurity.com/2025/07/09/kanvas-open-source-incident-response-case-management-tool/ — desktop-based (Python) IR case-management tool, gepubliceerd juli 2025; lichtgewicht alternatief.
- **GRR Rapid Response** — https://github.com/google/grr — Apache-2.0 remote live-forensics framework (v4.0.0.0, 15 dec 2025); ouder/zwaarder dan Velociraptor, dat als modernere opvolger geldt.
- **Timesketch** — https://github.com/google/timesketch — collaboratieve forensische tijdlijn-analyse (Google); dekt RS.AN; integreert met Plaso/OpenRelik.
- **OpenRelik** — https://openrelik.org/ · https://github.com/openrelik — modulair collaboratief DFIR-workflowplatform (Google/OSDFIR); orkestreert collectie → tijdlijn.
- **Plaso / log2timeline** — artifact-parsing-engine onder Timesketch; super-timeline-generatie.
- **IntelOwl / MISP** — observable-/threat-intel-verrijking die op DFIR-IRIS aansluit (hoofd-uitwerking hoort in IDENTIFY/DETECT).

---

## 2. SOAR / playbook-automatisering

Drie volwassen open-source SOAR-opties, elk met een ander profiel. **Shuffle** = breedste, volledig open
security-SOAR. **Tracecat** = AI-native (open-core). **StackStorm** = meest permissief (Apache-2.0) maar
DevOps-georiënteerd en vertragend tempo.

### 2.1 Shuffle — *primaire aanbeveling RESPOND / SOAR-orkestratie*

1. **Naam + URL:** Shuffle — https://github.com/Shuffle/Shuffle · https://shuffler.io
2. **CSF-functie(s):** RESPOND (RS.MI mitigatie-automatisering, RS.CO notificatie-workflows, RS.MA orkestratie). Raakt DETECT (alert-handling).
3. **Capability:** Visuele no-code/low-code security-orkestratie (SOAR): playbook-workflows die tools koppelen en acties automatiseren.
4. **Omschrijving:** Vaak omschreven als "open-source Tines" / "IFTTT voor cybersecurity". Puur orkestratie
   (geen SIEM). Genereert integraties automatisch uit OpenAPI-specs → zeer brede tool-connectiviteit.
   Populair in MSSP/SOC-omgevingen. Optionele managed cloud (zelfde codebase).
5. **Rijpheid:** **Hoog.** v2.2.1 (12 mei 2026); RC v2.2.2-rc1 (27 mei 2026). Actieve ontwikkeling, honderden
   community-apps, ~2.3k sterren.
6. **Licentie:** **Dual: AGPL-3.0-only (core) + MIT (workflows/apps/SDK/docs).** **Volledig open source** —
   geen proprietary enterprise-tier, geen gated features. (Beide OSI-goedgekeurd.)
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar (Docker Compose, on-prem). Cloud is optioneel, niet vereist.
8. **Integreerbaarheid:** REST API; app-ecosysteem op OpenAPI-spec → auto-generatie van integraties voor
   elk OpenAPI-tool. Sterke koppelbaarheid.
9. **AI-native koppelbaarheid:** Deels. Geen ingebouwde LLM-actie-engine; AI bereikbaar via workflow-apps
   (bv. OpenAI-app uit OpenAPI). Geen native agent-runtime.
10. **Stack/taal:** Go (backend), ReactJS (frontend), Python (app-SDK/integraties). Docker Compose.
11. **Fit-score: 5/5.** Rijpste, volledig open-source, security-first SOAR met breedste integratielaag en
    zonder betaalmuur. Eerste keuze voor playbook-automatisering in de blueprint.
12. **Bronnen:**
    - https://github.com/Shuffle/Shuffle · https://github.com/Shuffle/Shuffle/releases (v2.2.1, mei 2026)
    - https://shuffler.io/ · https://aimultiple.com/open-source-soar

---

### 2.2 Tracecat — *aanbeveling voor AI-native SOAR (open-core — let op betaalmuur)*

1. **Naam + URL:** Tracecat — https://github.com/TracecatHQ/tracecat · https://www.tracecat.com
2. **CSF-functie(s):** RESPOND (RS.MI/RS.MA automatisering + case management, RS.CO). Raakt DETECT.
3. **Capability:** "Agentic security automation" — workflow-automatisering + case management + AI-agents in één platform.
4. **Omschrijving:** Open-source alternatief voor Tines/Splunk SOAR met uitgesproken AI-first identiteit.
   No-code (drag-and-drop) én code-driven (YAML/Python) met versiebeheer/CI-CD. 500+ integraties.
   Sandboxing via nsjail; Temporal voor workflow-betrouwbaarheid. Jongste en snelst bewegende van de drie.
5. **Rijpheid:** **Middel–hoog (jong).** 1.0.0-beta.49 (15 juni 2026); meerdere RC-cycli per week. Zeer
   actief, maar nog beta — let op stabiliteits-/breaking-change-risico voor productie.
6. **Licentie:** **Open-core.** Core = **AGPL-3.0-only** (geverifieerd in root-LICENSE). ⚠️ Achter de
   betaalmuur (Enterprise Edition, dir `packages/tracecat-ee`, proprietary; `deployments/k8s` = PolyForm
   Shield, source-available): **RBAC, SCIM, geavanceerde/`preset` AI-agents (100+ MCP-servers), MCP-
   inventory, AI-dashboards, Kubernetes-Helm, skills-registry.** Community-tier (self-host, AGPL) dekt
   basis-workflows + `ai.agent`.
7. **EU-soevereiniteit:** ✅ Self-host community-tier mogelijk (Docker Compose). ⚠️ Kubernetes-deployment en
   delen van EE zitten achter source-available/proprietary licenties; AI-agents gebruiken externe LLM-API's
   (Anthropic/OpenAI = non-EU) — dataresidentie per koppeling beoordelen.
8. **Integreerbaarheid:** REST API + **native MCP-server** (Claude Code / Copilot / Codex kunnen automation bouwen). CLI/YAML/Python-workflows.
9. **AI-native koppelbaarheid:** **Ja (sterkste van het veld).** Native `ai.agent`-actie (prompt + tool-
   allowlist, autonome tool-calls), multi-provider (Anthropic/OpenAI, bring-your-own-LLM), human-in-the-loop
   `tool_approvals`, configureerbare `max_tool_calls`/`max_requests`, audit-trail van prompts/tool-calls.
10. **Stack/taal:** Python (backend), TypeScript (frontend), HCL (infra). Temporal, nsjail. Docker/Fargate/K8s.
11. **Fit-score: 4/5.** Enige SOAR met ingebouwde, govern- en audit-bare AI-agents (past op de "AI bereidt
    voor, mens beslist"-lijn). Min: open-core (RBAC/SCIM betaald) en beta-status. Sterke kandidaat voor
    AI-native vCISO-scenario's, met expliciete open-core-waarschuwing.
12. **Bronnen:**
    - https://github.com/TracecatHQ/tracecat · https://github.com/TracecatHQ/tracecat/blob/main/LICENSE (AGPL-3.0 core geverifieerd)
    - https://docs.tracecat.com/agents/ai-agent · https://www.tracecat.com/pricing

---

### 2.3 StackStorm — *aanbeveling waar Apache-2.0 / event-driven gewenst is*

1. **Naam + URL:** StackStorm — https://github.com/StackStorm/st2 · https://stackstorm.com
2. **CSF-functie(s):** RESPOND (RS.MI/RS.MA automatisering, RS.CO ChatOps-notificatie). Bredere ops-/SRE-scope.
3. **Capability:** Event-driven automatiseringsplatform ("IFTTT voor Ops"): triggers → rules → actions/workflows.
4. **Omschrijving:** Volwassen, breed inzetbaar automatiseringsplatform (oorsprong Netflix). DevOps/SRE-
   georiënteerd, maar veel engineering-geleide securityteams bouwen er custom SOAR mee. ChatOps (Slack/Teams).
5. **Rijpheid:** **Hoog maar vertragend.** v3.9.0 (10 okt 2025) was de enige 2025-release (gat van ~2 jaar
   sinds v3.8.1). Grootste community (~6.5k sterren, 160 packs, 6000+ acties), maar geen commerciële motor
   die nieuwe features aanjaagt → ⚠️ momentum-/onderhoudsrisico.
6. **Licentie:** **Apache-2.0** (OSI-goedgekeurd, permissief). **Volledig open source**, geen closed enterprise-tier (meest permissieve optie van de drie).
7. **EU-soevereiniteit:** ✅ Zelf-hostbaar (Linux-only). Geen SaaS-verplichting. Vereist MongoDB/RabbitMQ + DB.
8. **Integreerbaarheid:** Volledige REST API (token-auth), CLI, 160 integration-packs (exchange.stackstorm.org).
9. **AI-native koppelbaarheid:** Deels/nee. Geen native AI; custom LLM-integratie bouwbaar als action-pack.
10. **Stack/taal:** Python. MongoDB + RabbitMQ + PostgreSQL/Redis. Linux-only.
11. **Fit-score: 3/5.** Meest permissieve licentie en battle-tested, maar DevOps-i.p.v.-security-focus, zware
    infra-footprint en vertragend tempo drukken de fit voor een security-eerst blueprint.
12. **Bronnen:**
    - https://github.com/StackStorm/st2 · https://github.com/StackStorm/st2/releases (v3.9.0, okt 2025)
    - https://docs.stackstorm.com/reference/api.html

> **Multi-functie / dedup-noot.** SOAR-tools (Shuffle, Tracecat, StackStorm) raken zowel **RESPOND** als
> **DETECT** (alert-orkestratie) en deels **PROTECT** (geautomatiseerde controls). Hoofd-uitwerking hier in
> RESPOND; in andere functie-documenten kruisverwijzen. Tracecat overlapt bovendien met case management (§1).

**Long tail — SOAR / orkestratie:**
- **SOARCA** — https://github.com/COSSAS/SOARCA — open-source CACAO-v2 security-orchestrator (COSSAS, NL/EU-herkomst); voert CACAO-playbooks uit → bruggetje §3.
- **n8n** — generieke workflow-automatisering, deels gebruikt als light-SOAR; let op licentie (Sustainable Use License = source-available, géén OSI-open-source) — niet als open-source SOAR aanmerken.
- **Walkoff / Tines (CE)** — geen geschikte volledig-open-source community-editie gevonden voor de blueprint.

---

## 3. IR-runbooks / playbook-bibliotheken (governance/proces)

Standaarden en bibliotheken die playbooks definiëren (i.t.t. de engines die ze uitvoeren). Het zwaartepunt
is verschoven naar **CACAO v2.0** als machine-leesbare convergentiestandaard. De community-taxonomieën
**ATC/RE&CT** zijn conceptueel sterk maar lijken stil te liggen.

### 3.1 CACAO Security Playbooks v2.0 (+ SOARCA) — *primaire aanbeveling RESPOND / playbook-standaard*

1. **Naam + URL:** OASIS CACAO Security Playbooks v2.0 — https://www.oasis-open.org/standard/cacao-security-playbooks-v2-0/ (orchestrator: SOARCA — https://github.com/COSSAS/SOARCA)
2. **CSF-functie(s):** RESPOND (RS.MA/RS.MI/RS.CO — gestandaardiseerde respons-course-of-action). Raakt DETECT/RECOVER.
3. **Capability:** Vendor-neutrale, machine-leesbare playbook-standaard (JSON-schema) voor detectie,
   containment, eradicatie en herstel — deelbaar en uitvoerbaar.
4. **Omschrijving:** OASIS-standaard die playbooks als reeks beveiligingsacties in een vendor-neutraal JSON-
   schema vastlegt. SOARCA (COSSAS, EU/NL) is een open-source CACAO-v2-orchestrator die playbooks valideert
   en uitvoert. Fraunhofer-onderzoek (mrt/apr 2025) toont meetbaar betere responsprestaties met
   gestandaardiseerde CACAO-playbooks, ook voor organisaties zonder groot securityteam.
5. **Rijpheid:** **Hoog (standaard) / opkomend (tooling).** CACAO v2.0 is vastgestelde OASIS-standaard;
   SOARCA actief. Groeiend ecosysteem en academische validatie.
6. **Licentie:** Standaard = open OASIS-specificatie (vrij implementeerbaar). SOARCA = open-source
   (verifieer exacte SPDX in https://github.com/COSSAS/SOARCA vóór gebruik).
7. **EU-soevereiniteit:** ✅ Standaard is locatie-onafhankelijk; SOARCA is EU-herkomst (COSSAS, NL) en zelf-hostbaar. Sterke EU-fit.
8. **Integreerbaarheid:** JSON-schema → tooling-onafhankelijk. Koppelt aan OpenC2 (commando-laag) als actie-stappen. SOARCA = uitvoeringslaag.
9. **AI-native koppelbaarheid:** Deels/ja. Machine-leesbaar JSON-schema leent zich uitstekend voor LLM-
   generatie/validatie van playbooks; CoSAI AI-IR-framework levert al CACAO-playbooks (zie §3, long tail).
10. **Stack/taal:** Specificatie (JSON). SOARCA: Go.
11. **Fit-score: 4/5.** Beste framework-agnostische, machine-leesbare playbook-standaard met groeiende open-
    source uitvoering (SOARCA) en EU-herkomst. Conceptuele ruggengraat voor de playbook-laag van de blueprint.
12. **Bronnen:**
    - https://www.oasis-open.org/standard/cacao-security-playbooks-v2-0/
    - https://github.com/COSSAS/SOARCA
    - https://www.fraunhofer.de/en/press/research-news/2025/april-2025/standardized-security-playbooks-improve-protection-against-cyberattacks.html

---

### 3.2 RE&CT-framework (+ ATC) — *aanbeveling als open respons-taxonomie/referentie*

1. **Naam + URL:** RE&CT — https://atc-project.github.io/atc-react/ · https://github.com/atc-project/atc-react (verwant: Atomic Threat Coverage — https://github.com/atc-project/atomic-threat-coverage)
2. **CSF-functie(s):** RESPOND (RS.AN/RS.MI — taxonomie van atomaire respons-acties). ATC raakt DETECT.
3. **Capability:** Open taxonomie van atomaire Incident-Response-technieken (Response Actions) + curated Response Playbooks; "ATT&CK voor verdedigers".
4. **Omschrijving:** RE&CT beschrijft en categoriseert atomaire IR-acties (mens-leesbaar Markdown +
   machine-leesbaar YAML), uitvoerbaar via o.a. TheHive case-templates. ATC is de detectie-/respons-
   analytics-tegenhanger (auto-generatie van wiki's, ATT&CK-Navigator-layers).
5. **Rijpheid:** **Laag/dormant.** Architectuur is solide en veel-gerefereerd, maar upstream-commits lijken
   schaars in 2025–2026. ⚠️ Behandel als referentie-/inspiratiebron, niet als levend onderhouden product.
6. **Licentie:** Open-source community-project (Apache-2.0-familie; verifieer per repo). Vrij te gebruiken/forken.
7. **EU-soevereiniteit:** ✅ Tekst-/YAML-content, locatie-onafhankelijk, volledig zelf te hosten.
8. **Integreerbaarheid:** YAML/Markdown → importeerbaar in case-management (TheHive-templates) en te mappen op CACAO.
9. **AI-native koppelbaarheid:** Deels. Gestructureerde YAML leent zich voor LLM-generatie van afgeleide playbooks.
10. **Stack/taal:** YAML + Markdown (content), Python (generatoren bij ATC).
11. **Fit-score: 3/5.** Waardevolle open respons-taxonomie als referentielaag bovenop CACAO, maar dormancy
    drukt de fit — gebruik als content-startpunt, niet als afhankelijkheid.
12. **Bronnen:**
    - https://atc-project.github.io/atc-react/ · https://github.com/atc-project/atc-react
    - https://blog.senthorus.ch/posts/react_framework/

---

**Long tail — playbooks / standaarden / content:**
- **CoSAI AI Incident Response Framework v1.0** — https://www.oasis-open.org/2025/11/18/coalition-for-secure-ai-releases-two-actionable-frameworks-for-ai-model-signing-and-incident-response/ — OASIS/CoSAI (nov 2025), eerste IR-framework voor AI-systemen, met CACAO-playbooks (prompt-injection, model-poisoning, agentic compromise). **Hoog relevant voor AI-native blueprint.**
- **OpenC2** — https://openc2.org/ — OASIS machine-to-machine commando-taal (executie-laag onder CACAO-playbook-stappen); vendor-neutraal.
- **Counteractive IR-plan-template** — https://github.com/counteractive/incident-response-plan-template — MIT-gelicenseerde scenario-playbooks (ransomware, phishing, identity) in Markdown.
- **GuardSight CIRT Playbook Battle Cards** — https://github.com/guardsight/gsvsoc_cirt-playbook-battle-cards — gestructureerde beslis-kaarten per incidenttype.
- **Incident Response Consortium playbooks** — https://www.incidentresponse.com/open-source-playbooks/ — gallery van gekoppelde E2E-playbooks (relaunch 2025).
- **Awesome Incident Response** — https://github.com/meirwah/awesome-incident-response — curated meta-lijst van IR-tools/resources.

---

## 4. Crisiscommunicatie / stakeholder-notificatie

Generieke open-source IR-communicatietooling. Geen security-specifiek "crisis-comms"-product domineert;
de praktijk combineert een **statuspagina** (externe stakeholders), een **incident-coördinatie-app**
(intern/Slack) en — EU-specifiek — **NIS2-meldtemplates**. Let op: alle drie de top-tools raken hooguit
indirect het security-domein; weeg ze als ondersteunend, niet als kern-IR.

### 4.1 Incident-coördinatie — *aanbeveling: "Response" (Monzo) / Incidental*

1. **Naam + URL:** Response (Monzo) — https://github.com/monzo/response · alternatief: Incidental
2. **CSF-functie(s):** RESPOND (RS.CO communicatie/coördinatie, RS.MA incident-coördinatie).
3. **Capability:** Automatiseert communicatie, coördinatie en rapportage tijdens incidenten (Slack-gedreven).
4. **Omschrijving:** Open-source Django-app van Monzo, gebouwd om incident-communicatie, taakverdeling en
   post-incident-rapportage te stroomlijnen vanuit Slack. Engineering-georiënteerd; goed te koppelen aan een
   case-managementsysteem (DFIR-IRIS) voor het security-spoor. Incidental biedt vergelijkbare functionaliteit
   (Slack-integratie, statuspagina's, custom workflows).
5. **Rijpheid:** **Middel.** Bewezen in productie (Monzo), maar geen security-specifiek product; afhankelijk van Slack.
6. **Licentie:** Open source (verifieer exacte SPDX per repo — Monzo Response historisch MIT-achtig). Geen betaalmuur.
7. **EU-soevereiniteit:** ⚠️ Zelf-hostbaar, maar Slack-afhankelijkheid (US-SaaS) verzwakt soevereiniteit; overweeg Mattermost/Teams-koppeling.
8. **Integreerbaarheid:** Slack-API-gedreven; REST/webhook-koppelbaar aan IR-tooling.
9. **AI-native koppelbaarheid:** Deels. Slack + webhook-flow laat LLM-samenvatting/timeline-generatie toe; geen native AI.
10. **Stack/taal:** Python (Django).
11. **Fit-score: 3/5.** Nuttige open-source incident-coördinatielaag, maar Slack-afhankelijkheid en niet-
    security-specifieke scope drukken de fit; positioneer als optionele comms-koppeling naast DFIR-IRIS.
12. **Bronnen:**
    - https://github.com/monzo/response · https://medevel.com/incident-and-case-management-1500/

---

### 4.2 Statuspagina / externe stakeholder-notificatie — *aanbeveling: OpenStatus / Uptime Kuma*

1. **Naam + URL:** OpenStatus — https://www.openstatus.dev/ (monitoring-variant met notificaties: Uptime Kuma — https://github.com/louislam/uptime-kuma)
2. **CSF-functie(s):** RESPOND (RS.CO — externe stakeholder-/klantcommunicatie tijdens incidenten).
3. **Capability:** Open-source statuspagina + incidentmeldingen/notificaties richting externe stakeholders.
4. **Omschrijving:** OpenStatus wordt in 2025–2026-vergelijkingen aangewezen als de actief-onderhouden
   opvolger van het gestagneerde **Cachet** (laatste release 2023). Uptime Kuma combineert monitoring met
   statuspagina's en notificaties via tientallen kanalen (e-mail, Telegram, Discord) — maar mist rijke
   gestructureerde incident-tijdlijn op de statuspagina (open feature-request). Kener/Upptime als alternatieven.
5. **Rijpheid:** **Hoog (beide actief in 2026).** Uptime Kuma breed gebruikt; OpenStatus moderne architectuur.
6. **Licentie:** Open source (Uptime Kuma = MIT; OpenStatus = open source — verifieer exacte SPDX per repo). Geen betaalmuur.
7. **EU-soevereiniteit:** ✅ Beide zelf-hostbaar (Docker), on-prem mogelijk; geen verplichte SaaS.
8. **Integreerbaarheid:** API + webhooks; veel notificatie-kanalen (Uptime Kuma). Koppelbaar aan IR-flow.
9. **AI-native koppelbaarheid:** Deels/nee. Geen native AI; statusberichten kunnen via API/LLM gegenereerd worden.
10. **Stack/taal:** OpenStatus: TypeScript/Next.js. Uptime Kuma: Node.js/Vue.
11. **Fit-score: 3/5.** Solide, zelf-hostbare externe-communicatielaag; niet security-specifiek en beperkte
    incident-tijdlijn-functies drukken de fit. Cachet expliciet afgeraden (gestagneerd).
12. **Bronnen:**
    - https://www.openstatus.dev/guides/best-opensource-status-page-2026 · https://github.com/louislam/uptime-kuma
    - https://statusgator.com/blog/7-cachet-alternatives-for-better-incident-communication/

---

### 4.3 NIS2-meldtemplates & GRC-incidentmodule — *aanbeveling: EU-meldtemplates + verinice/nis2-toolkits*

1. **Naam + URL:** NIS2 common incident reporting templates (ENISA/NIS2 Cooperation Group) — https://www.enisa.europa.eu/publications/nis2-technical-implementation-guidance · open toolkits: verinice (https://verinice.com/en/solutions/domains/nis-2-directive), nis2-public (https://github.com/fabriziosalmi/nis2-public)
2. **CSF-functie(s):** RESPOND (RS.CO — wettelijke incidentmelding/communicatie). Raakt GOVERN (compliance).
3. **Capability:** Gestandaardiseerde EU-meldtemplates + open-source workflows/GRC-modules voor NIS2-incidentmelding (24u/72u/eindrapport).
4. **Omschrijving:** De NIS2 Cooperation Group stelde op 26 mei 2026 gemeenschappelijke incident-reporting-
   templates vast; de Europese Commissie werkt aan een single-entry-point. Open-source ondersteuning:
   **verinice** (GRC-tool met NIS2-module: incident management, TOM's, rapportage), **nis2-public**
   (continuous-posture-platform met IR-workflows + deadline-countdowns), **nis2-sme-toolkit** (MKB-compliance).
5. **Rijpheid:** **Opkomend (regelgeving 2026–2027 in beweging).** Templates net vastgesteld; deadlines
   (CSIRT-referent dec 2026, 24h-notificatie jan 2027) maken dit actueel maar in flux. ⚠️ Volg ENISA-updates.
6. **Licentie:** Templates = open EU-publicatie. verinice = open source (community-editie; verifieer SPDX).
   nis2-public/-sme-toolkit = open source op GitHub (verifieer SPDX per repo).
7. **EU-soevereiniteit:** ✅✅ Expliciet EU-georiënteerd; verinice (DE) en EU-templates; zelf-hostbaar. Sterkste EU-fit van §4.
8. **Integreerbaarheid:** Templates = document/JSON; verinice = import/export + API; nis2-toolkits = workflow/script-based.
9. **AI-native koppelbaarheid:** Deels. Gestructureerde templates lenen zich voor LLM-ondersteund invullen/concept-melding (mens beslist/verzendt).
10. **Stack/taal:** verinice: Java. nis2-toolkits: gemengd (Python/scripts/docs).
11. **Fit-score: 4/5 (EU-context).** Voor een EU/overheid-vCISO-blueprint is dit de meest relevante
    communicatielaag: wettelijk verankerd, EU-soeverein, open. Min: jong/in-flux en deels GRC- i.p.v. IR-tooling.
12. **Bronnen:**
    - https://www.enisa.europa.eu/publications/nis2-technical-implementation-guidance
    - https://eunewsletter.eu/nis2-cooperation-group-adopts-common-templates-for-incident-reporting/
    - https://verinice.com/en/solutions/domains/nis-2-directive · https://github.com/fabriziosalmi/nis2-public

---

**Long tail — communicatie/notificatie:**
- **Cachet** — https://github.com/cachethq/cachet — ⚠️ historische open-source statuspagina, ontwikkeling **gestagneerd** (laatste release 2023); afgeraden voor nieuwe projecten.
- **Kener / Upptime** — moderne open-source statuspagina-alternatieven (GitHub-gebaseerd, actief).
- **Keep** — https://openalternative.co/alternatives/incident-io — open-source alert-/incident-hub die alerts uit meerdere bronnen centraliseert.
- **Aurora (Arvo AI)** — https://www.arvoai.ca/blog/incident-io-alternative-open-source — Apache-2.0 incident.io-alternatief met AI-onderzoek, werkt met lokale LLM (Ollama); jong, verifieer maturiteit.
- **nis2-sme-toolkit** — https://github.com/paolocarner/nis2-sme-toolkit — praktische NIS2-compliance-toolkit voor MKB.

---

## 5. Niet-gedekt / gaps

- **Geheugen-/disk-forensics & malware-analyse** (Volatility, YARA, Cuckoo/CAPE) — wel RESPOND-relevant
  (RS.AN), maar bewust niet uitgewerkt; hoort grotendeels bij de DFIR/DETECT-laag. Aanbevolen vervolg.
- **Geautomatiseerde containment/EDR-respons** (OpenEDR, Wazuh active-response, osquery) — raakt RS.MI; Wazuh
  hoort primair in DETECT. Cross-functie dedup met DETECT/PROTECT vereist.
- **Werkelijk EU-soeverein incident-comms-platform** — gat. De comms-laag (§4) leunt op US-SaaS (Slack) of
  niet-security-specifieke statuspagina's. Geen volwassen, security-eerst, EU-soeverein crisis-comms-OSS
  gevonden; verinice + EU-NIS2-templates zijn de beste benadering, maar dekken vooral de *wettelijke* melding.
- **Native AI-agent-SOAR buiten open-core** — Tracecat is de enige met ingebouwde AI-agents, maar RBAC/SCIM/
  preset-agents zitten achter de betaalmuur. Een volledig-open, AI-native SOAR met RBAC ontbreekt (juni 2026).
- **TheHive-vervanging-volledigheid** — DFIR-IRIS dekt case management, maar de oude TheHive+Cortex+MISP-
  drie-eenheid is niet 1-op-1 vervangen; integratie-glue (DFIR-IRIS ↔ Cortex ↔ MISP) vergt eigen werk.
- **Velociraptor-/SOARCA-licentie 1-op-1** — AGPL/open-source uit secundaire bronnen bevestigd, maar niet in
  dit onderzoek rechtstreeks uit het repo-LICENSE-bestand gelezen; verifieer SPDX vóór adoptie.

---

### Dedup-register (multi-functie tools — niet dubbel uitwerken)

| Tool | Primair | Ook | Hoofd-uitwerking in |
|------|---------|-----|---------------------|
| Velociraptor | RESPOND (RS.AN/MI) | DETECT | RESPOND §1.3 |
| Timesketch / GRR / OpenRelik / Plaso | RESPOND (RS.AN) | DETECT | RESPOND long tail (of DETECT) |
| Cortex | RESPOND (RS.AN) | DETECT | RESPOND §1.2 |
| Shuffle / StackStorm | RESPOND (SOAR) | DETECT, PROTECT | RESPOND §2 |
| Tracecat | RESPOND (SOAR + case) | DETECT | RESPOND §2.2 (overlapt §1) |
| MISP / IntelOwl | IDENTIFY/DETECT (TI) | RESPOND (verrijking) | IDENTIFY/DETECT |
| Wazuh | DETECT | RESPOND (active-response RS.MI) | DETECT |
| CACAO / OpenC2 / RE&CT | RESPOND (playbooks) | DETECT/RECOVER | RESPOND §3 |
| verinice / nis2-toolkits | RESPOND (RS.CO melding) | GOVERN (compliance) | RESPOND §4.3 (raakt GOVERN) |
