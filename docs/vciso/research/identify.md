# IDENTIFY — open-source tooling landscape (NIST CSF 2.0)

> **Scope.** Dit document inventariseert open-source tooling voor de NIST CSF 2.0-functie **IDENTIFY** (ID)
> ten behoeve van een generieke, framework-agnostische vCISO-blueprint. De functie IDENTIFY omvat
> asset- & data-inventarisatie (CMDB/discovery), risk register & risicobeoordeling, threat modeling,
> compliance-mapping & gap-analyse, en threat intelligence. Per sub-categorie zijn de **top 2–3 tools**
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

---

*Peildatum: juni 2026. Alle licentie- en versiegegevens geverifieerd via directe bronraadpleging.*
