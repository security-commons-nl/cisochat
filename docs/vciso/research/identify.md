# IDENTIFY — open-source tooling landscape (NIST CSF 2.0)

> **Scope.** Dit document inventariseert open-source tooling voor de NIST CSF 2.0-functie **IDENTIFY** (ID)
> ten behoeve van een generieke, framework-agnostische vCISO-blueprint. De functie IDENTIFY omvat
> asset- & data-inventarisatie (CMDB/discovery), risk register & risicobeoordeling, threat modeling,
> compliance-mapping & gap-analyse, threat intelligence, en extern aanvalsoppervlak-discovery (ASM).
> Per sub-categorie zijn de **top 2–3 tools**
> volledig uitgewerkt (12-velden scorekaart); overige vondsten staan als *long tail* (naam + URL + 1 zin).
> Harde poort: **alléén open source** — open-core wordt beoordeeld op uitsluitend de community-editie,
> met expliciete vermelding van wat achter de betaalmuur zit. Licentie-vallen (BSL/SSPL/Commons Clause/
> CC-NC/source-available) worden expliciet benoemd; OSI-goedkeuring is de norm.
> EU-soevereiniteit is een zachte weging (zelf-hostbaarheid + dataresidentie).
> Alle tool-claims zijn voorzien van ≥1 bron-URL. Peildatum onderzoek: **juni 2026**.

---

## 1. Asset- & data-inventory (CMDB / discovery)

Actief beheer van het asset-universum is de basis van IDENTIFY. Twee tools domineren het open-source
landschap: **NetBox** voor netwerk- en infrastructuur-CMDB, **Ralph** voor data-center-DCIM en lifecycle-
management. OCS Inventory NG vult aan als agent-gebaseerde software-/hardware-discovery. De rest van
het landschap is overwegend open-core of minder actief.

### 1.1 NetBox — *primaire aanbeveling IDENTIFY / asset inventory*

1. **Naam + URL:** NetBox — https://github.com/netbox-community/netbox
2. **CSF-functie(s):** IDENTIFY (primair: ID.AM asset management). Raakt ook PROTECT (RBAC, change log voor audit).
3. **Capability:** Netwerk-CMDB, IP-adresbeheer (IPAM), data-center-infrastructuur-management (DCIM), asset source-of-truth.
4. **Omschrijving:** De facto open-source standaard voor netwerk- en infrastructuur-CMDB. Beheert racks,
   devices, kabels, IP-adressen, VLANs, circuits en stroomcircuits. Uitbreidbaar via plugins; beschikt over
   Jinja2-templates voor device-configuratie en event-gebaseerde automation. Volledige changelog per object
   met gebruikersattributie. Opgericht door DigitalOcean, nu onafhankelijk community-project.
5. **Rijpheid:** **Hoog.** v4.6.3 uitgebracht 16 juni 2026. 20.9k GitHub-sterren, 3k forks, 421 watchers.
   Meerdere release per maand; grote, actieve community.
6. **Licentie:** Apache-2.0 (OSI-goedgekeurd, permissief). Geen copyleft. NetBox Cloud en NetBox Enterprise
   zijn commerciële aanbiedingen; de core software blijft volledig open source zonder functiebeperkingen.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar on-premises of in eigen cloud. Geen verplichte cloud-
   afhankelijkheid of SaaS-component. Dataresidentie 100% in eigen beheer.
8. **Integreerbaarheid:** REST API + GraphQL API out-of-the-box. Uitgebreide plugin-architectuur. CLI via
   `pynetbox` Python-client. Integraties beschikbaar met Ansible, Terraform, Nautobot en security-tooling
   (o.a. runZero voor discovery-import).
9. **AI-native koppelbaarheid:** Deels. REST/GraphQL API maakt LLM-integratie technisch goed mogelijk; geen
   native MCP-server beschikbaar (juni 2026), maar gestructureerde JSON-output leent zich goed voor
   AI-pipelines. Community-plugin netbox-mcp-server bestaat als experimenteel project.
10. **Stack/taal:** Python (Django backend), JavaScript (Vue.js frontend). PostgreSQL database.
11. **Fit-score: 5/5.** Rijpst beschikbare open-source CMDB; permissieve licentie; EU-zelf-hostbaar; actieve
    community; uitstekende API. Meest geschikte keuze als asset source-of-truth voor vCISO-blueprint.
12. **Bronnen:**
    - https://github.com/netbox-community/netbox (release v4.6.3, juni 2026)
    - https://netboxlabs.com/blog/netbox-labs-platform-foundation-ot-asset-inventory/
    - https://help.runzero.com/docs/netbox/ (integratie runZero → NetBox)

---

### 1.2 Ralph — *aanbeveling voor data-center DCIM & lifecycle*

1. **Naam + URL:** Ralph — https://github.com/allegro/ralph
2. **CSF-functie(s):** IDENTIFY (ID.AM asset lifecycle). Secundair: GOVERN (asset ownership & verantwoording).
3. **Capability:** Full-lifecycle asset management (aankoop → decommission), DCIM (rek-visualisatie, netwerkapparatuur), CMDB voor datacenters en back-offices.
4. **Omschrijving:** Gebouwd door Allegro (Poolse e-commerce) voor eigen datacenter-operaties, daarna open
   source vrijgegeven. Beheert zowel fysieke (servers, netwerk) als niet-fysieke (licenties, SaaS) assets.
   Flexibel workflow-systeem voor asset-statusovergangen. Native DC-visualisatie (rekken, layouts).
   Allegro publiceert de broncode maar neemt zelf weinig externe bijdragen aan; community-gebruik is welkom.
5. **Rijpheid:** **Hoog.** Release 20260609.1 (9 juni 2026 — datumgebaseerde versioning). 2.5k sterren, 590
   forks. Allegro gebruikt Ralph actief in productie, wat de kwaliteitsdruk hoog houdt. Externe contributor-
   community is kleiner dan NetBox.
6. **Licentie:** Apache-2.0 (OSI-goedgekeurd, permissief). Geen open-core constructie.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar. Geen SaaS-afhankelijkheid. Polish/EU-herkomst (Allegro).
8. **Integreerbaarheid:** REST API aanwezig. Geen officiële CLI of MCP-server. Integreerbaar met monitoring-
   tooling via API. Minder omvangrijke integratie-ecosysteem dan NetBox.
9. **AI-native koppelbaarheid:** Deels. REST API beschikbaar; gestructureerde data-output; geen native MCP.
10. **Stack/taal:** Python (Django). PostgreSQL.
11. **Fit-score: 4/5.** Sterke tool voor DC-gerichte omgevingen; permissief; EU-zelf-hostbaar; actief in
    productie. Lager dan NetBox door kleinere community en minder integraties. Complementair aan NetBox
    (Ralph = lifecycle + DC-visualisatie; NetBox = netwerk source-of-truth).
12. **Bronnen:**
    - https://github.com/allegro/ralph (release 20260609.1)
    - https://virima.com/blog/top-open-source-it-asset-management-software (overzicht 2026)

---

### Long tail — asset & CMDB

- **OCS Inventory NG** (https://github.com/ocsinventory-ng / https://www.ocsinventory-ng.com/en) —
  Agent-gebaseerde hardware/software-discovery; GPLv2; actief (reworked branch met REST API in ontwikkeling
  per 2026); goed voor endpoint-discovery maar minder geschikt als CMDB source-of-truth.
- **Snipe-IT** (https://github.com/grokability/snipe-it) — Free/open source IT asset & licentie-management;
  AGPL-3.0; 11k+ sterren; primair gericht op hardware-lifecycle en licenties, niet op netwerk-CMDB; goede API.
- **GLPI** (https://github.com/glpi-project/glpi) — ITSM + CMDB + inventaris; GPLv3; rijp en breed ingezet,
  met name in Franstalige overheidsomgevingen; meer gericht op helpdesk/ITSM dan puur CMDB.
- **CMDBuild** (https://www.cmdbuild.org/) — Open source web-CMDB configureerbaar op maat; AGPL-3.0;
  Italiaanse herkomst; rijp maar niche-community; goed voor maatwerk-schemas.

---

## 2. Risk register & risicobeoordeling

De open-source GRC-ruimte is dunner dan de commerciële markt. Twee tools verdienen volledige analyse:
**CISO Assistant** (reeds uitgewerkt in govern.md — zie dedup-noot) en **MONARC** als dedicated
risk-assessment-methodologie. SimpleRisk dekt de pure risk-register use-case.

> **Dedup-noot:** CISO Assistant (https://github.com/intuitem/ciso-assistant-community) is ook bij
> GOVERN volledig uitgewerkt (govern.md §1.1). Voor IDENTIFY/risk-register geldt dezelfde scorekaart;
> deze wordt hier niet herhaald maar geldt als primaire aanbeveling voor gecombineerde GRC+risk-functie.

### 2.1 MONARC — *aanbeveling voor gestructureerde risico-analyse*

1. **Naam + URL:** MONARC — https://github.com/monarc-project/MonarcAppFO — https://www.monarc.lu/
2. **CSF-functie(s):** IDENTIFY (ID.RA risk assessment, ID.AM asset-risico-koppeling). Raakt ook GOVERN (risk governance).
3. **Capability:** Gestructureerde, methodologische risicobeoordeling (kwalitatief en kwantitatief); risk register; aanbevelingsbeheer; rapportage.
4. **Omschrijving:** MONARC (Method for an Optimised aNAlysis of Risks) is ontwikkeld door de Luxembourg
   House of Cybersecurity (NC3-LU/CASES-LU). De methodologie stelt organisaties in staat herhaalbare
   risicoanalyses te doen door generalisatie van risicopatronen vanuit eerdere analyses ("gebruik wat anderen
   al hebben gedaan"). Ondersteunt assets, dreigingen, kwetsbaarheden en risicoscenario's. RESTful API met
   OpenAPI 3.0-documentatie. Sterke EU-verankering (Luxemburgse overheidsinstelling).
5. **Rijpheid:** **Midden–hoog.** v2.13.4 uitgebracht 27 maart 2026; 87 releases totaal; actieve ontwikkeling.
   126 GitHub-sterren (kleine maar gerichte community). Relatief niche buiten EU/Benelux-overheidsomgeving.
6. **Licentie:** AGPL-3.0 (OSI-goedgekeurd, sterk copyleft). Copyleft-implicatie: modificaties die als
   service aangeboden worden moeten open source worden vrijgegeven. Geen open-core.
7. **EU-soevereiniteit:** ✅✅ Uitstekend. Ontwikkeld door EU-overheidsinstelling (Luxemburg); volledig zelf-
   hostbaar; actief onderhouden door NC3-LU; ook beschikbaar via eugit.opencloud.lu (EU-git-infrastructuur).
8. **Integreerbaarheid:** RESTful API (OpenAPI 3.0). Import/export van risicomodellen. Koppelbaar met
   MISP voor threat intelligence. CLI niet standaard aanwezig.
9. **AI-native koppelbaarheid:** Deels. OpenAPI-documentatie maakt integratie technisch haalbaar; geen native
   MCP of LLM-connector aanwezig (juni 2026).
10. **Stack/taal:** PHP (36%), Shell (53%). MariaDB/MySQL database.
11. **Fit-score: 4/5.** Sterkste EU-verankerde, methodologisch onderbouwde open-source risicoanalysetool.
    Hoge EU-soevereiniteit, actief onderhouden door overheidsinstelling. Nadelen: PHP-stack is minder modern;
    kleine community; AGPL-copyleft vereist aandacht bij integratie in proprietaire omgevingen.
12. **Bronnen:**
    - https://github.com/monarc-project/MonarcAppFO (release v2.13.4, maart 2026)
    - https://securitymadein.lu/services/monarc-1/ (CASES-LU/NC3-LU projectpagina)
    - https://www.monarc.lu/publications/risk-assessment-optimisation-with-monarc/

---

### 2.2 SimpleRisk — *aanbeveling voor pure risk-register functie*

1. **Naam + URL:** SimpleRisk — https://github.com/simplerisk/code — https://www.simplerisk.com/
2. **CSF-functie(s):** IDENTIFY (ID.RA risk assessment, risk register). Beperkte GOVERN-dekking (risk governance).
3. **Capability:** Risk register, risicobeoordeling, risicobehandeling, rapportage.
4. **Omschrijving:** SimpleRisk richt zich uitsluitend op risicobeheersing — geen volledig GRC-platform.
   De core biedt risico-identificatie, beoordeling (kwalitatief), behandelworkflows, en dashboards.
   Modulaire architectuur: core is open source, uitbreidingen ("Extras") zijn betaald. Mozilla Public
   License 2.0, actief onderhouden. UI-verbeteringen en rapportage zijn aanzienlijk verbeterd in 2025.
5. **Rijpheid:** **Midden–hoog.** Actief project (vroeg 2010s tot heden); regelmatige releases. 15 GitHub-
   repositories beschikbaar. Community relatief klein ten opzichte van bredere GRC-tools.
6. **Licentie:** Mozilla Public License 2.0 (OSI-goedgekeurd, zwak copyleft / file-level). Core is volledig
   open source. De betaalde "Extras" zijn proprietary add-ons — **niet** open source.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar on-premises. Geen verplichte SaaS-component voor core.
8. **Integreerbaarheid:** REST API is een **betaald Extra** (niet beschikbaar in open source core). CLI niet
   aanwezig. Dit is een significant nadeel voor automatisering en AI-integratie vanuit de gratis editie.
9. **AI-native koppelbaarheid:** Nee (vanuit open source core). API vereist betaalde module.
10. **Stack/taal:** PHP. MySQL/MariaDB.
11. **Fit-score: 3/5.** Solide en gefocuste risk-register tool met OSI-licentie; nadeel is dat API achter
    betaalmuur zit (beperkt automatisering), PHP-stack, en beperkte compliance-mapping vs. CISO Assistant.
    Geschikt als lightweight risk-only oplossing; minder geschikt als centraal GRC-platform.
12. **Bronnen:**
    - https://github.com/simplerisk/code (MPL-2.0 licentie)
    - https://www.simplerisk.com/blog/simplerisk-free-and-open-source-vs-fully-featured-platform
    - https://infosecflow.com/blog/open-source-grc-comparison/ (vergelijking 2026)

---

### Long tail — risk register & GRC

- **Eramba** (https://www.eramba.org/) — ⚠️ **LICENTIE-VAL:** Niet OSI-open source. Eramba is
  source-available met custom proprietary licentie (geen redistribuutierechten). Officieel noemen ze
  het "hybrid" maar het voldoet niet aan de OSI Open Source Definition. Gebruik is gratis; code zit in
  Docker-images. Niet opnemen als open-source tool; wél vermelden als gratis-maar-proprietary optie.
  Bron: https://discussions.eramba.org/t/question-eramba-not-anymore-open-source/2506
- **GovReady-Q** (https://github.com/GovReady/govready-q) — Apache-2.0; OSI-goedgekeurd; OSCAL/OpenControl-
  gebaseerd; gericht op US-federale ATO-processen; laatste release oktober 2022 — **project lijkt inactief**
  (laag sterrencount 215, geen recente releases). Niet aanbevolen voor actieve inzet.
- **OpenFAIR implementaties** — Geen geconsolideerde, actieve open-source implementatie van het FAIR
  kwantitatief risicomodel beschikbaar als kant-en-klare tool (juni 2026). Losse scripts/notebooks bestaan,
  maar geen rijp platform.

---

## 3. Threat modeling

Threat modeling is een specifieke discipline binnen IDENTIFY: het vroegtijdig modelleren van
beveiligingsdreigingen in systemen en architecturen. Drie open-source tools verdienen aandacht.

### 3.1 OWASP Threat Dragon — *primaire aanbeveling voor diagram-gebaseerd threat modeling*

1. **Naam + URL:** OWASP Threat Dragon — https://github.com/OWASP/threat-dragon — https://www.threatdragon.com/
2. **CSF-functie(s):** IDENTIFY (ID.RA risicobeoordeling via threat modeling). Raakt GOVERN (vroegtijdige risicoherkenning).
3. **Capability:** Visueel, diagram-gebaseerd threat modeling (DFDs); automatische dreigingssuggesties; rapportage.
4. **Omschrijving:** OWASP Production-project. Biedt een grafische editor voor data-flow-diagrammen (DFD)
   met ingebouwde dreigingssuggesties op basis van STRIDE-methodologie. Beschikbaar als web-applicatie
   en desktop-applicatie (Windows, macOS, Linux). Ondersteunt opslag in lokaal bestandssysteem, GitHub,
   GitLab, Bitbucket en GitHub Enterprise. Vue.js frontend met Node.js backend. OWASP-keurmerk garandeert
   community-governance.
5. **Rijpheid:** **Midden–hoog.** v2.6.2 uitgebracht 10 mei 2026. 1.5k GitHub-sterren. Actief onderhouden
   onder OWASP-governance. Kleiner contributor-team dan grote commerciële alternatieven.
6. **Licentie:** Apache-2.0 (OSI-goedgekeurd, permissief). Volledig open source, geen enterprise-editie.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar (web-applicatie on-premises of desktop). Geen SaaS-
   afhankelijkheid verplicht. Data blijft lokaal of in eigen VCS.
8. **Integreerbaarheid:** REST API aanwezig (web-versie). Threat Model File (TMF) format — JSON-gebaseerd,
   gestandaardiseerd formaat. Plannen voor TMF-interoperabiliteit met andere tools in v3.x. CLI niet standaard.
9. **AI-native koppelbaarheid:** Deels. TMF/JSON-output is gestructureerd en leent zich voor AI-analyse.
   Geen native MCP-server (juni 2026). Community-experimenten met AI-dreigingssuggesties via API in roadmap.
10. **Stack/taal:** JavaScript/Node.js (backend), Vue.js (frontend).
11. **Fit-score: 4/5.** Sterkste open-source keuze voor diagram-gebaseerd threat modeling; OWASP-governance;
    permissieve licentie; EU-zelf-hostbaar; actief. Nadeel: beperkte interoperabiliteit met pytm/Threagile
    (TMF-formaat is eigen formaat, wijziging gepland voor v3.x).
12. **Bronnen:**
    - https://github.com/OWASP/threat-dragon (release v2.6.2, mei 2026)
    - https://owasp.org/www-project-threat-dragon/
    - https://github.com/OWASP/threat-dragon/wiki/Threat-Model-File-(TMF)-format

---

### 3.2 Threagile — *aanbeveling voor code/YAML-gebaseerd agile threat modeling*

1. **Naam + URL:** Threagile — https://github.com/Threagile/threagile — https://threagile.io/
2. **CSF-functie(s):** IDENTIFY (ID.RA architectuur-risicobeoordeling). Geschikt voor DevSecOps-pipelines.
3. **Capability:** YAML-gebaseerde architectuurmodellering met geautomatiseerde risicoregels; PDF/Excel/JSON-rapportage; CI/CD-integratie.
4. **Omschrijving:** "Agile Threat Modeling Toolkit" die architectuur-as-code mogelijk maakt: het systeem
   wordt beschreven als YAML-bestand (in IDE of editor), waarna Threagile automatisch risicoregels evalueert
   en rapporten genereert (PDF, Excel, JSON, DFD-diagrammen). Custom risicoregels via YAML-scripts (geen
   Go-compilatie vereist). Server-modus met REST API. Uitstekend voor DevSecOps-teams die threat modeling
   willen integreren in CI/CD-pipelines.
5. **Rijpheid:** **Midden.** v0.9.1 uitgebracht 30 juli 2024. 768 sterren, 167 forks, 32 watchers. Actief
   maar kleinere community. Versienummer suggereert pre-1.0 stabiliteit. Nieuwste activiteit: 2024.
6. **Licentie:** MIT (OSI-goedgekeurd, permissief). Geen copyleft, geen open-core.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar (Docker-container of standalone). Geen externe afhankelijkheden.
8. **Integreerbaarheid:** REST API (server-modus). CLI (Docker-gebaseerd). JSON/YAML-output; goed integreerbaar
   in CI/CD-pipelines (GitHub Actions, GitLab CI).
9. **AI-native koppelbaarheid:** Ja. YAML + JSON-output is schoon gestructureerd; REST API maakt LLM-
   integratie eenvoudig. Geen native MCP maar architectuur leent zich uitstekend voor AI-orchestratie.
10. **Stack/taal:** Go (97%). Docker-first deployment.
11. **Fit-score: 4/5.** Sterkste keuze voor DevSecOps/as-code threat modeling; permissieve licentie; EU-zelf-
    hostbaar; uitstekende AI-koppelbaarheid via gestructureerde output. Nadeel: kleinere community, pre-1.0
    versienummer, minder geschikt voor niet-technische gebruikers die een GUI prefereren.
12. **Bronnen:**
    - https://github.com/Threagile/threagile (release v0.9.1, juli 2024)
    - https://www.iriusrisk.com/resources-blog/recommended-threat-modeling-tools

---

### 3.3 pytm (OWASP) — *aanbeveling voor programmatorisch/code-first threat modeling*

1. **Naam + URL:** pytm — https://github.com/OWASP/pytm
2. **CSF-functie(s):** IDENTIFY (ID.RA dreigings- en kwetsbaarheidsmodellering). Geschikt voor developer-first omgevingen.
3. **Capability:** Python-library voor programmatisch threat modeling; automatische DFD- en sequence-diagram-generatie; CAPEC-gebaseerde dreigingscatalogus.
4. **Omschrijving:** OWASP Production-project. pytm laat ontwikkelaars een systeem beschrijven als Python-code
   (object-georiënteerd, `object.property = value`), waarna automatisch een dreigingsrapport gegenereerd
   wordt, inclusief DFD (via Graphviz) en sequence-diagrammen (via PlantUML). Dreigingscatalogus gebaseerd
   op CAPEC (MITRE). "Shift-left": threat modeling zo vroeg mogelijk in de SDLC integreren.
5. **Rijpheid:** **Midden.** v1.3.1 uitgebracht 25 april 2024. 1.1k sterren, 222 forks. Actief onderhouden
   onder OWASP; OpenSSF Best Practices badge aanwezig. 36 open issues en 5 open PRs (2024-2026). Laatste
   release in april 2024 — minder frequent dan Threat Dragon.
6. **Licentie:** MIT (OSI-goedgekeurd, permissief). CAPEC-content onder aparte MITRE-licentie (research/
   development gebruik toegestaan).
7. **EU-soevereiniteit:** ✅ Pure Python-library, geen externe diensten vereist. Draait volledig lokaal.
8. **Integreerbaarheid:** Python-library (pip-installeerbaar). Output: Graphviz DOT, PlantUML, HTML, JSON.
   Goed integreerbaar in CI/CD-pipelines. Geen REST API (is een library, geen service).
9. **AI-native koppelbaarheid:** Deels. Gestructureerde Python-objecten en JSON-output leent zich voor AI-
   pipelines; als library direct aanroepbaar vanuit AI-agents. Geen MCP-server.
10. **Stack/taal:** Python 3.
11. **Fit-score: 3/5.** Sterke keuze voor developer-teams die threat modeling als code willen; permissieve
    licentie; EU-zelf-hostbaar. Nadeel: vereist Python-kennis; geen GUI; minder recent actief dan Threat Dragon.
    Complementair aan Threat Dragon (pytm = code-first; Threat Dragon = GUI-first).
12. **Bronnen:**
    - https://github.com/OWASP/pytm (release v1.3.1, april 2024)
    - https://owasp.org/www-project-pytm/
    - https://devguide.owasp.org/en/04-design/01-threat-modeling/02-pytm/

---

### Long tail — threat modeling

- **Microsoft Threat Modeling Tool** — ⚠️ **GEEN open source.** Gratis te downloaden maar proprietary
  Microsoft-software. Niet opnemen als open-source tool.
- **IriusRisk Community Edition** — ⚠️ Beoordeling onzeker. IriusRisk is primair commercieel; een
  "community edition" wordt soms vermeld maar licentievoorwaarden zijn onduidelijk / source-available.
  Twijfel expliciet benoemd — verificatie vereist voor eventuele opname.
- **drawio + TMAC** — (https://github.com/xerocraft/tmac) — Combinatie van draw.io diagramming met
  Threat Modeling as Code; MIT-licentie; experimenteel/niche; laag sterrencount.
- **OWASP Threat Model Library** (https://owasp.org/www-project-threat-model-library/) — Geen tool maar
  een bibliotheek van herbruikbare dreigingspatronen; complementair aan Threat Dragon/pytm.

---

## 4. Compliance-mapping & gap-analyse

CISO Assistant is de absolute koploper in deze categorie (zie ook govern.md §1.1 voor volledige
scorekaart). Hier wordt de tool beknopt herhaald met focus op IDENTIFY-specifieke toepassingen.

### 4.1 CISO Assistant — *primaire aanbeveling compliance-mapping & gap-analyse*

> **Dedup-noot:** Volledige 12-velden scorekaart staat in govern.md §1.1. Onderstaande is een
> IDENTIFY-gerichte samenvatting.

1. **Naam + URL:** CISO Assistant Community — https://github.com/intuitem/ciso-assistant-community
2. **CSF-functie(s):** GOVERN (primair), IDENTIFY (compliance gap-analyse, risk register). Dekt alle CSF-functies via framework-mapping.
3. **Capability:** 150+ frameworks automatisch cross-mapped; gap-analyse; compliance-scoring; risk assessment.
4. **Omschrijving:** AGPL-3.0 GRC-platform met automatische control-mapping tussen frameworks (ISO 27001,
   NIST CSF 2.0, NIS2, DORA, BIO2, GDPR, CIS, SOC 2, HIPAA e.v.a.). Gap-analyse: één scope evalueren tegen
   meerdere frameworks tegelijk. v3.18.1 uitgebracht 15 juni 2026. 4.1k sterren.
5. **Rijpheid:** Hoog. v3.18.1 (juni 2026). Actief, frequent gereleaset.
6. **Licentie:** AGPL-3.0 (OSI). Enterprise-directory met proprietary Commercial Software License — niet open source. Community-editie volledig functioneel.
7. **EU-soevereiniteit:** ✅ Zelf-hostbaar; intuitem is Frans bedrijf (EU).
8. **Integreerbaarheid:** REST API (in community-editie). Import/export. API-first design.
9. **AI-native koppelbaarheid:** Ja. REST API + gestructureerde output. Actieve AI-integratie-roadmap.
10. **Stack/taal:** Python (Django backend), SvelteKit frontend.
11. **Fit-score: 5/5** — zie govern.md voor onderbouwing.
12. **Bronnen:** https://github.com/intuitem/ciso-assistant-community — https://infosecflow.com/blog/open-source-grc-comparison/

---

### Long tail — compliance-mapping & gap-analyse

- **OpenControl / Compliance Masonry** (https://github.com/opencontrol/compliance-masonry) —
  CC0-1.0 licentie (public domain); YAML-gebaseerde compliance-as-code; sterk gericht op US-federale
  ATO/FedRAMP-processen; beperkte EU-relevantie; project relatief stabiel maar niche.
- **GovReady-Q** (https://github.com/GovReady/govready-q) — Apache-2.0; OSCAL-gebaseerd; laatste release
  oktober 2022 — **project lijkt inactief**; niet aanbevolen voor actieve inzet (zie ook §2 long tail).
- **VerifyWise** (https://github.com/verifywise/verifywise) — Nieuw open-source GRC-platform (2024);
  MIT-licentie; gericht op AI-governance (EU AI Act); vroeg stadium maar veelbelovend voor AI-specifieke
  compliance; te volgen als aanvulling op CISO Assistant voor AI-regelgeving.

---

## 5. Threat intelligence (CTI)

Threat intelligence voedt IDENTIFY met contextuele dreigingsinformatie. Twee platforms domineren de
open-source ruimte: **MISP** (de facto standaard voor dreigingsdeling) en **OpenCTI** (modernere
kennisgraaf-aanpak). AIL Framework vult aan voor OSINT/leak-analyse.

### 5.1 MISP — *primaire aanbeveling threat intelligence*

1. **Naam + URL:** MISP — https://github.com/MISP/MISP — https://www.misp-project.org/
2. **CSF-functie(s):** IDENTIFY (ID.RA threat intelligence). Raakt DETECT (signaaldeling) en RESPOND (incident-CTI).
3. **Capability:** Threat intelligence platform; IOC-deling en -correlatie; feeds; STIX-import/export; REST API; community-netwerk.
4. **Omschrijving:** De facto open-source standaard voor threat intelligence sharing. Gecentraliseerde
   opslag en correlatie van indicatoren en dreigingsdata. Real-time synchronisatie tussen MISP-instanties
   met granulaire sharing-controles (communities, organisaties, classificaties). Machine-readable export
   (STIX2, IDS-formaten, JSON) en import uit meerdere standaarden. Ingebouwde workflow-automatisering,
   REST API met PyMISP-library. Ontwikkeld door CIRCL (Luxembourg CERT). Open source commitment geborgd
   via geïnterlocked licentie-structuur: geen enkele partij kan de licentie eenzijdig wijzigen.
   v2.5.41 uitgebracht 17 juni 2026.
5. **Rijpheid:** **Hoog.** 6.4k sterren, 1.6k forks, 281 watchers. Actief onderhouden sinds 2012.
   Kernteam bij CIRCL (LU); brede internationale contributor-community. v2.5-branch (2025) leverde
   major UI-overhaul en modernisering.
6. **Licentie:** AGPL-3.0 (OSI-goedgekeurd, sterk copyleft). Geen open-core. Geen enkele commerciële
   partij kan licentie wijzigen (contributor license agreement). Volledig community-eigendom.
7. **EU-soevereiniteit:** ✅✅ Uitstekend. CIRCL = Luxemburgse overheidsinstelling; volledig zelf-hostbaar
   (on-premises, Docker, VM); actief onderhouden voor digitale soevereiniteit. Geen SaaS-verplichtingen.
8. **Integreerbaarheid:** Uitgebreide REST API; PyMISP Python-client; STIX2-import/export; integraties
   met Splunk, TheHive, OpenCTI, Cortex, SIEM-platforms, IDS/IPS-systemen. Feedsysteem voor externe CTI.
9. **AI-native koppelbaarheid:** Ja. REST API + gestructureerde STIX2/JSON-output; PyMISP als Python-client
   direct bruikbaar in AI-pipelines. Geen native MCP-server (juni 2026) maar technisch goed koppelbaar.
10. **Stack/taal:** PHP (backend), Python (tooling/PyMISP). MariaDB/MySQL database.
11. **Fit-score: 5/5.** De rijpste, meest breed inzetbare open-source CTI-tool. Sterke EU-verankering
    (CIRCL/LU); AGPL-geborgd geen vendor lock-in; uitstekende integratie-ecosysteem. AGPL-copyleft vereist
    aandacht bij integratie in proprietaire producten maar is geen bezwaar voor interne vCISO-inzet.
12. **Bronnen:**
    - https://github.com/MISP/MISP (release v2.5.41, juni 2026)
    - https://www.misp-project.org/2025/12/31/misp.2025-welcome-2026.html/
    - https://en.wikipedia.org/wiki/MISP_Threat_Sharing

---

### 5.2 OpenCTI — *aanbeveling voor kennisgraaf-gebaseerde CTI*

1. **Naam + URL:** OpenCTI — https://github.com/OpenCTI-Platform/opencti — https://filigran.io/platform/opencti/
2. **CSF-functie(s):** IDENTIFY (ID.RA threat intelligence, kennisbeheer). Raakt DETECT en RESPOND.
3. **Capability:** Kennisgraaf voor cyber threat intelligence; STIX2-datamodel; actor/campagne/vulnerability-tracking; GraphQL API; visualisaties.
4. **Omschrijving:** Modern CTI-platform gebaseerd op STIX2-kennisgraaf; beheert dreigingsactoren,
   campagnes, malware, kwetsbaarheden en indicatoren in gestructureerde relaties. Volledige GraphQL API.
   Integraties met MISP, TheHive, VirusTotal, Shodan en 100+ connectors. v7.260615.0 uitgebracht juni 2026.
   Ontwikkeld door Filigran (Frans bedrijf, EU). 9.6k sterren, 1.4k forks.
5. **Rijpheid:** **Hoog.** Zeer actief (379 releases); grote community; breed ingezet bij overheids-SOCs
   en grote organisaties. Community Edition Apache-2.0; Enterprise Edition met proprietary functies.
6. **Licentie:** **Open-core.** Community Edition: Apache-2.0 (OSI-goedgekeurd, permissief). Enterprise
   Edition: proprietary Filigran-licentie. Achter betaalmuur: SSO, geavanceerde RBAC, audit-logging,
   full-text search (CE = metadata-only), geavanceerde workflow-automatisering, SaaS-deployment,
   multi-tenancy. CE is functioneel bruikbaar maar mist enterprise-hardening features.
7. **EU-soevereiniteit:** ✅ Zelf-hostbaar via Docker. Filigran = Frans bedrijf (EU); air-gap deployment
   ondersteund. SaaS-optie beschikbaar maar niet verplicht. Goed voor EU-soevereiniteitseis.
8. **Integreerbaarheid:** GraphQL API (primair); REST API aanwezig; 100+ connectors beschikbaar; STIX2-
   standaard garandeert interoperabiliteit. Python-client beschikbaar. Integreerbaar met MISP, TheHive, SIEM.
9. **AI-native koppelbaarheid:** Ja. GraphQL + gestructureerde STIX2-output; actieve AI-features in roadmap
   (Enterprise: AI-analysefuncties). CE biedt goede basis voor AI-integratie.
10. **Stack/taal:** TypeScript (69%), JavaScript (23%), Python (7%). Elasticsearch/OpenSearch + Redis + RabbitMQ.
11. **Fit-score: 4/5.** Rijpste kennisgraaf-gebaseerde CTI-tool; moderne stack; uitstekende API; EU-herkomst.
    Eén serieus bezwaar: open-core met relevante functies (SSO, full-text search) achter betaalmuur in
    Enterprise Edition. Voor vCISO-blueprint: CE volstaat voor het merendeel van use-cases.
12. **Bronnen:**
    - https://github.com/OpenCTI-Platform/opencti (release v7.260615.0, juni 2026)
    - https://docs.opencti.io/latest/administration/enterprise/ (Enterprise vs. CE featurevergelijking)
    - https://filigran.io/blog/upgrading-to-opencti-enterprise-edition/

---

### Long tail — threat intelligence

- **AIL Framework** (https://github.com/ail-project/ail-framework) — AGPL-3.0; OSI-goedgekeurd; ontwikkeld
  door CIRCL (LU); modulair framework voor OSINT-analyse en informatielekinspectie (paste sites, dark web,
  chats); export naar MISP; actief onderhouden met EU/HOPLITE-project financiering; niche gebruik (OSINT/
  leak-analyse) maar EU-verankerd en complementair aan MISP.
- **IntelOwl** (https://github.com/intelowlproject/IntelOwl) — AGPL-3.0; OSI-goedgekeurd; aggregeert CTI
  via 100+ analyzers (VirusTotal, MISP, etc.); REST API; actief onderhouden; goed voor IOC-verrijking.
- **Cortex** (https://github.com/TheHive-Project/Cortex) — AGPL-3.0; OSI-goedgekeurd; observable-analyse
  en response-automatisering; onderdeel van TheHive-ecosysteem; complementair aan MISP/OpenCTI.

---

## 6. Extern aanvalsoppervlak-discovery (ASM/EASM)

§1 dekt de **binnenkant** van het asset-universum: CMDB, IPAM, agent-discovery. Deze paragraaf dekt de
**buitenkant**: wat ziet een aanvaller zonder enige toegang? Voor lokale overheden is dat een reële
blinde vlek, omdat het aanvalsoppervlak versnipperd is over eigen netblokken, hosters, SaaS en
projectsites die niemand meer beheert. Een CMDB die alleen vult wat de organisatie zelf aanmeldt,
mist per definitie de vergeten omgevingen. Externe discovery is juist daar het controlemiddel:
het toetst zelfrapportage aan waarneembare werkelijkheid.

Het open-source landschap is hier ruimer dan bij GRC. **OWASP Amass** is de rijpste losse tool, de
**ProjectDiscovery-suite** de sterkste pijplijn-benadering, en **IVRE** het enige project dat de
volledige Shodan-functie in eigen beheer benadert.

### 6.1 OWASP Amass — *primaire aanbeveling extern aanvalsoppervlak*

1. **Naam + URL:** OWASP Amass — https://github.com/owasp-amass/amass — https://owasp.org/www-project-amass/
2. **CSF-functie(s):** IDENTIFY (ID.AM asset-inventarisatie vanaf de buitenkant, ID.RA blootstellingsanalyse). Raakt DETECT: periodieke herhaling signaleert nieuw opgekomen blootstelling.
3. **Capability:** OSINT-gedreven mapping van het externe aanvalsoppervlak: subdomein-enumeratie, DNS-, certificaat- en ASN-analyse, opbouw van een doorzoekbare asset-graaf.
4. **Omschrijving:** OWASP-project en de facto open-source tegenhanger van commerciële EASM-diensten.
   Combineert tientallen passieve bronnen (CT-logs, passive DNS, web-archieven, zoekmachines) met
   optionele actieve verificatie. Versie 5 is een architectuurherbouw: de datastructuur zit nu in
   aparte repo's (`open-asset-model` voor het model, `asset-db` voor opslag), waardoor de uitkomst een
   bevraagbare graaf is in plaats van een platte lijst. Dat maakt herhaalde runs vergelijkbaar, wat
   voor een vCISO belangrijker is dan de eenmalige vondst.
5. **Rijpheid:** **Hoog.** 14.954 sterren, 2.167 forks. v5.1.1 uitgebracht 7 april 2026; v5.0.0 op
   3 augustus 2025; laatste commit-activiteit 19 juli 2026. Release-cadans is laag (v4.2.0 dateert van
   september 2023), maar de sprong naar v5 was een volledige herbouw en het project is aantoonbaar actief.
6. **Licentie:** **Apache-2.0** (OSI-goedgekeurd, permissief). Geen open-core, geen betaalde editie.
   ⚠️ *Verificatienoot:* GitHub toont bij deze repo "NOASSERTION". Dat komt doordat het `LICENSE`-bestand
   opent met een copyrightregel ("Copyright 2017-2026 Jeff Foley. All rights reserved. License: Apache2.0")
   bóven de licentietekst, waardoor de automatische detectie afhaakt. De tekst zelf is onverkort de
   Apache License 2.0, en alle bijbehorende org-repo's (`open-asset-model`, `asset-db`, `resolve`, `docs`)
   staan expliciet op Apache-2.0. Dit is dus géén licentie-val, maar wel een geval waar een directory
   die alleen het GitHub-label leest de verkeerde conclusie trekt.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar (binary of Docker), database blijft lokaal.
   Kanttekening: de dekking van de passieve bronnen hangt af van API-sleutels bij externe partijen
   (veelal VS). Zonder sleutels werkt de tool, met minder resultaat. De query's zelf gaan dan wel
   naar die derden, wat bij gebruik op eigen gemeentelijke domeinen een bewuste keuze vraagt.
8. **Integreerbaarheid:** CLI-first. JSON-output; `asset-db` (SQLite of PostgreSQL) is direct met SQL
   te bevragen. Geen REST-service in de kern, dus koppelen gebeurt via de database of de output.
9. **AI-native koppelbaarheid:** Deels. Gestructureerde JSON plus een bevraagbare graaf zijn goed
   AI-koppelbaar; geen native MCP-server (peildatum augustus 2026).
10. **Stack/taal:** Go. SQLite/PostgreSQL voor `asset-db`.
11. **Fit-score: 5/5.** Rijpste open-source ASM-tool, permissief gelicentieerd, OWASP-governance,
    zelf-hostbaar, en met v5 een datamodel dat herhaalmeting mogelijk maakt. Beste startpunt voor het
    ASM-component van de blueprint.
12. **Bronnen:**
    - https://github.com/owasp-amass/amass (v5.1.1, april 2026; 14.954 sterren, geverifieerd 09-08-2026)
    - https://github.com/owasp-amass/amass/blob/master/LICENSE (Apache-2.0-tekst)
    - https://github.com/owasp-amass/open-asset-model · https://github.com/owasp-amass/asset-db (beide Apache-2.0)

---

### 6.2 ProjectDiscovery-suite — *aanbeveling voor pijplijn- en CI-gedreven ASM*

1. **Naam + URL:** subfinder, httpx, naabu, nuclei, asnmap — https://github.com/projectdiscovery
2. **CSF-functie(s):** IDENTIFY (ID.AM/ID.RA externe inventarisatie en blootstelling). `nuclei` raakt nadrukkelijk DETECT en PROTECT (kwetsbaarheidsdetectie).
3. **Capability:** Modulaire keten: `asnmap` (ASN naar netblokken, scope-bepaling) → `subfinder` (passieve subdomein-enumeratie) → `httpx` (HTTP-probing en fingerprinting) → `naabu` (poortscan) → `nuclei` (template-gebaseerde checks).
4. **Omschrijving:** Geen platform maar losse Unix-achtige tools die op elkaar aansluiten via stdin/stdout
   en JSON. Precies dat maakt ze geschikt voor een vCISO-pijplijn: elke stap is los te vervangen, te
   loggen en te herhalen, en het geheel draait ongewijzigd in een cron-job of CI-pipeline. `nuclei` is
   met 30k sterren het zwaartepunt van het ecosysteem en heeft een grote, community-onderhouden
   templatecollectie.
5. **Rijpheid:** **Hoog**, en dit is de actiefste familie in dit hele document. Peildatum 9 augustus 2026:
   `nuclei` v3.11.1 (8 aug 2026, 30.395 sterren) · `subfinder` v2.15.0 (5 aug 2026, 14.159) ·
   `httpx` v1.10.0 (9 juli 2026, 10.255) · `naabu` v2.6.1 (5 mei 2026, 6.166) · `asnmap` (1.115,
   commit-activiteit 5 aug 2026). Alle vijf onge-archiveerd en wekelijks actief.
6. **Licentie:** **MIT** voor alle vijf (OSI-goedgekeurd, permissief). Naast de tools bestaat een
   commercieel cloud-platform (ProjectDiscovery Cloud Platform), maar dat is een *laag ernaast*, geen
   open-core-uitholling: de CLI's zijn volledig functioneel zonder account, en cloud-upload is een
   expliciete opt-in-vlag (`-dashboard`, `-auth`). Wie die vlaggen niet gebruikt, stuurt niets weg.
   Aandachtspunt voor beleid: de vlaggen bestaan wél, dus leg vast dat ze uit blijven.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar, single binaries, geen verplichte dienst.
   Zelfde kanttekening als bij Amass: `subfinder` bevraagt externe bronnen, dus het passieve deel lekt
   de gezochte domeinnamen naar derden tenzij je de bronnenlijst beperkt.
8. **Integreerbaarheid:** Uitstekend. Alle tools zijn ook als Go-library te gebruiken; `-json`-output
   overal; ontworpen voor ketening. `nuclei`-templates zijn YAML en dus zelf te schrijven en te reviewen.
9. **AI-native koppelbaarheid:** **Ja, sterkste van de drie.** Schone JSON per stap, deterministische
   CLI-aanroepen en een tekstueel templateformaat: dit is de kandidaat die zich het beste laat
   MCP-wrappen voor een vCISO-dirigent. Geen officiële MCP-server (peildatum augustus 2026).
10. **Stack/taal:** Go (alle vijf).
11. **Fit-score: 4/5.** Permissief, extreem actief, en qua orchestreerbaarheid de beste fit voor een
    AI-gedreven blueprint. Eén punt aftrek omdat het geen samenhangend product is: inventaris, historie
    en rapportage moet je zelf bouwen bovenop de output. Complementair aan Amass (Amass = graaf en
    herhaalmeting; ProjectDiscovery = pijplijn en verificatie).
12. **Bronnen:**
    - https://github.com/projectdiscovery/subfinder · /httpx · /naabu · /nuclei · /asnmap (versies en
      sterrentallen geverifieerd via de GitHub-API op 09-08-2026)
    - https://github.com/projectdiscovery/nuclei#readme (cloud-tier als opt-in beschreven)

---

### 6.3 IVRE — *aanbeveling voor een zelf-gehoste Shodan-achtige functie*

1. **Naam + URL:** IVRE — https://github.com/ivre/ivre — https://ivre.rocks/
2. **CSF-functie(s):** IDENTIFY (ID.AM externe asset-database, ID.RA blootstelling). Raakt DETECT (passieve sensordata, passive DNS).
3. **Capability:** Recon-framework dat eigen scandata en externe bronnen samenbrengt in één doorzoekbare database met web-UI: netwerkinventaris, passive DNS, flow-analyse, en een eigen EASM-view.
4. **Omschrijving:** Waar Amass en de ProjectDiscovery-tools losse meetinstrumenten zijn, is IVRE de
   *bewaarlaag*: het slikt output van Nmap, Masscan, Zeek, p0f en de ProjectDiscovery-tools en maakt
   daar een bevraagbare database van. De projectbeschrijving is expliciet dat dit de architectuur is
   om "je eigen, volledig zelf-beheerde alternatief voor Shodan, ZoomEye, Censys en GreyNoise" te
   bouwen. Voor een gemeente die niet afhankelijk wil zijn van een Amerikaanse SaaS is dit het meest
   directe antwoord, tegen de prijs van eigen bouw- en beheerinspanning.
5. **Rijpheid:** **Midden–hoog.** 4.109 sterren, 699 forks. Laatste getagde release v0.9.21 dateert van
   25 september 2024, maar de hoofdlijn loopt gewoon door: commits van 5 en 26 juli 2026 (upload-pagina
   in de web-UI, database-fixes), laatste push 5 augustus 2026. Praktische consequentie: wie IVRE
   inzet draait feitelijk vanaf `main` of een container, niet vanaf de laatste tag. Dat is een reëel
   beheersrisico dat expliciet belegd moet worden.
6. **Licentie:** **GPL-3.0** (OSI-goedgekeurd, sterk copyleft). Geen open-core, geen betaalde editie.
   Copyleft-implicatie: afgeleide distributies moeten onder GPL-3.0 vrijgegeven worden. Voor interne
   inzet bij een gemeente geen bezwaar; wél relevant als Commons er een product omheen zou bouwen.
7. **EU-soevereiniteit:** ✅✅ Uitstekend. Frans project, volledig zelf-hostbaar, en het enige in deze
   paragraaf waarbij de data-verzameling zelf in eigen beheer kan blijven (eigen scans, eigen sensoren)
   zonder query's naar derden.
8. **Integreerbaarheid:** Python-library plus CLI plus web-UI en REST-API. Slikt Nmap-XML, Masscan,
   Zeek-logs en ProjectDiscovery-output. MongoDB, PostgreSQL, SQLite en Elasticsearch als backends.
9. **AI-native koppelbaarheid:** Deels. Python-library is direct aanroepbaar vanuit een agent en de
   database is bevraagbaar; geen native MCP-server (peildatum augustus 2026).
10. **Stack/taal:** Python. MongoDB (primair), alternatief PostgreSQL/SQLite/Elasticsearch.
11. **Fit-score: 4/5.** Enige open-source antwoord op de Shodan-functie als geheel, sterke EU-positie,
    OSI-copyleft. Aftrek voor de trage release-cadans en de bouw- en beheerlast: dit is infrastructuur,
    geen tool die je in een middag draait.
12. **Bronnen:**
    - https://github.com/ivre/ivre (GPL-3.0; v0.9.21 sep 2024; commits juli 2026; geverifieerd 09-08-2026)
    - https://ivre.rocks/ (projectpositionering als zelf-gehoste Shodan/Censys-tegenhanger)

---

### Long tail — ASM

Alle onderstaande gegevens zijn op 09-08-2026 geverifieerd via de GitHub-API (licentie, laatste release,
laatste activiteit).

- **theHarvester** (https://github.com/laramies/theHarvester) — OSINT-verzameling van e-mailadressen,
  subdomeinen en namen uit publieke bronnen; v4.11.1 (juni 2026), 16.988 sterren, activiteit op de dag
  van verificatie. ⚠️ Licentie-noot: er staat géén `LICENSE`-bestand in de repo-root, waardoor GitHub
  geen licentie toont; `pyproject.toml` verklaart **GPL-2.0-only**. Bruikbaar, maar de licentie is
  minder hard vastgelegd dan bij de drie hierboven.
- **massdns** (https://github.com/blechschmidt/massdns) — GPL-3.0; bulk-DNS-resolver; 3.627 sterren;
  activiteit april 2026. Geen ASM-tool op zichzelf maar de bouwsteen onder snelle subdomein-enumeratie.
- **asnmap** (https://github.com/projectdiscovery/asnmap) — MIT; ASN naar CIDR-mapping; 1.115 sterren;
  actief. Klein maar precies wat je nodig hebt om de scope van een ASM-run te onderbouwen ("welke
  netblokken zijn eigenlijk van ons?").
- **SpiderFoot** (https://github.com/smicallef/spiderfoot) — MIT; 20.126 sterren, de bekendste naam in
  deze lijst; automatiseert OSINT over 200+ modules met web-UI. ⚠️ **Stagnatie:** laatste release v4.0
  dateert van april 2022, laatste commit-activiteit april 2026. Het commerciële vervolg (SpiderFoot HX)
  heeft de aandacht overgenomen. Sterrental is hier dus een misleidende rijpheidsindicator; niet
  aanbevelen zonder eigen onderhoudsafspraak.
- **Sudomy** (https://github.com/screetsec/Sudomy) — MIT; shell-gebaseerde subdomein-enumeratie;
  2.418 sterren; **laatste activiteit juni 2024**, feitelijk stil. Alleen noemen voor volledigheid.
- **crt.sh** (https://crt.sh) — publieke Certificate-Transparency-zoekdienst, gratis, en nog steeds de
  goedkoopste betrouwbare bron voor subdomein- en certificaatinventarisatie. Correctie op de eerdere
  notitie in dit document: het is niet alleen een dienst maar heeft ook een **open stack**. De
  broncode staat onder https://github.com/crtsh (`certwatch_db`, `cert_processor`, `ctlint`,
  `ctloglists`), alle **GPL-3.0** en actief (commits mei tot augustus 2026). De dienst wordt beheerd
  door Sectigo. Praktisch: gebruik de publieke dienst, maar weet dat zelf draaien mogelijk is.

---

### Licentie-vallen en niet-open alternatieven bij ASM

- ⚠️ **Sn1per Community Edition** (https://github.com/1N3/Sn1per) — **géén open source**, ondanks
  10.742 sterren en publieke broncode. `LICENSE.md` is een EULA van Sn1perSecurity LLC die verbiedt om
  de code te her-licentiëren, te hernoemen of er een product of dienst van af te leiden (betaald óf
  gratis), naamsvermelding verplicht stelt, en waarin de leverancier zich het recht voorbehoudt de
  voorwaarden eenzijdig te wijzigen en de licentie te beëindigen. Voldoet niet aan de OSI Open Source
  Definition en valt daarmee buiten de harde poort van dit onderzoek, net als Eramba (§2) en de
  Microsoft Threat Modeling Tool (§3). Dit is de belangrijkste licentie-val in deze categorie, juist
  omdat de tool in commerciële directory's zonder kanttekening tussen de gratis ASM-tools staat.
- **Shodan** (https://www.shodan.io) is inhoudelijk sterk (passieve banner-database over de IPv4-ruimte,
  Monitor-alerts op eigen netblokken, API en CLI) maar **volledig proprietary SaaS**: geen broncode,
  geen zelf-hosting, data in de VS. Wel vermelden als gratis-tot-goedkoop meetinstrument, niet opnemen
  als blueprint-component. Zelfde beoordeling voor **Censys**, **BinaryEdge**, **Netlas**, **ZoomEye**
  en **FOFA**. Aandachtspunt bij alle zes: de resultaten zijn versie-banner-matching op een
  momentopname, dus een *signaal* en geen *bevinding*. Toetsing tegen de werkelijke configuratie blijft
  nodig voordat er conclusies aan hangen.
- **Geen tool, wel relevant:** de **Shadowserver Foundation** (https://www.shadowserver.org) levert
  netwerkeigenaren kosteloos dagrapporten over blootgestelde en gecompromitteerde systemen binnen hun
  eigen ASN/CIDR. Voor Nederlandse gemeenten loopt zulke signalering deels via NCSC/IBD. Vóór je een
  ASM-component in een blueprint opneemt, hoort de vraag: komt dit al binnen via een bestaand kanaal?

### Grens die bij deze categorie hoort

Passief opzoeken raakt het doelsysteem niet en is daarmee iets anders dan actief scannen (`naabu`,
`nuclei`, Nmap en Masscan raken het wél). Voor alles wat actief is geldt: alleen op eigen assets of
met aantoonbare opdracht. Vondsten bij derden horen via een CVD-route, niet via een e-mail met een
screenshot. Voor een vCISO-blueprint betekent dit dat de ASM-pijplijn een expliciete scope-definitie
(zie `asnmap`, §6.2) als eerste stap hoort te hebben, niet als nagedachte.

---

## Niet-gedekt / gaps

Na dit brede onderzoek zijn de volgende witte vlekken geïdentificeerd:

### Kwantitatieve risicobeoordeling (OpenFAIR)
Geen volwassen, actief open-source platform beschikbaar dat het FAIR-model (Factor Analysis of Information
Risk) kwantitatief implementeert. Er bestaan losse Python-scripts en Jupyter-notebooks (bijv.
`pyfair`: https://github.com/theonaunheim/pyfair) maar geen productieklaar GRC-platform. Organisaties
die kwantitatieve risicoanalyse willen doen met open source tooling moeten dit zelf bouwen of uitwijken
naar spreadsheet-gebaseerde benaderingen.

### OT/ICS-asset discovery
NetBox ondersteunt OT-assets (NetBox Labs heeft een OT-blog), maar gespecialiseerde OT/ICS-CMDB-
tools (voor SCADA, ICS, PLC-inventarisatie) zijn dun bezaaid in de open-source ruimte. **Dragonfly**
en vergelijkbare tools zijn commercieel; **Claroty/Armis** zijn volledig proprietary. Gap: geen
volwassen open-source OT-asset-discovery-tool.

### Geautomatiseerde SBOM-integratie in risk-register
Software Bill of Materials (SBOM) tooling (Syft, Grype) bestaat als open source, maar de koppeling
van SBOM naar een risk-register (kwetsbaarheden per component → risicoscore in GRC-tool) is nog niet
kant-en-klaar beschikbaar. Dit vereist maatwerk-integratie.

### Threat intelligence voor OT/ICS
MISP en OpenCTI zijn IT-georiënteerd. Gespecialiseerde open-source CTI voor OT-dreigingen (bijv.
ICS-STIX-profielen, MITRE ATT&CK for ICS-integratie) is beperkt beschikbaar. Gedeeltelijk
gedekt via MISP-modules, maar niet als volwaardig OT-CTI-platform.

### AI-governance specifiek (EU AI Act / DORA)
CISO Assistant ondersteunt EU AI Act-mapping (framework aanwezig), maar gespecialiseerde open-source
tooling voor AI-governance (model-risicobeoordeling, AI-system-inventarisatie) is nog embryonaal.
**VerifyWise** (MIT, vroeg stadium) is de enige veelbelovende kandidaat.

### Continue ASM-monitoring als kant-en-klaar product

De categorie zelf is niet langer een gap: §6 dekt hem met drie bron-geverifieerde tools. Wat er
binnen die categorie níet is, is een open-source equivalent van **Shodan Monitor**: een dienst die
je eigen netblokken permanent bewaakt en alarmeert bij nieuwe blootstelling, zonder dat je er zelf
infrastructuur voor optuigt. Amass en de ProjectDiscovery-tools zijn meetinstrumenten die je zelf
moet inplannen, versioneren en vergelijken; IVRE (§6.3) levert de bewaarlaag maar vraagt eigen bouw
en beheer. Het verschil tussen "we hebben de tools" en "we merken het als er morgen iets nieuws
online staat" is hier dus nog steeds werk. Voor een vCISO-blueprint is dat juist het interessante
deel, want het is precies de orchestratie-taak die de dirigent kan invullen.

Tweede, hardere grens: de **passieve internetbrede bannerdekking** van Shodan/Censys is niet
open-source te repliceren zonder zelf de IPv4-ruimte te scannen, wat voor een gemeente noch
proportioneel noch wenselijk is. Wie die dekking wil, koopt hem of gebruikt hem niet.

---

*Peildatum: juni 2026. Alle licentie- en versiegegevens geverifieerd via directe bronraadpleging.*
*§6 (extern aanvalsoppervlak/ASM) toegevoegd op 09-08-2026; licentie, laatste release en activiteit*
*van alle genoemde repo's op die datum geverifieerd via de GitHub-API, niet via een tooldirectory.*
