# DETECT — open-source tooling landscape (NIST CSF 2.0)

> **Scope.** Dit document inventariseert open-source tooling voor de NIST CSF 2.0-functie **DETECT** (DE)
> ten behoeve van een generieke, framework-agnostische vCISO-blueprint. De functie DETECT omvat continue
> monitoring (DE.CM) en adverse-event-analyse (DE.AE): security posture / CSPM, vulnerability management,
> SIEM/monitoring, en detection-as-code / detectie-engineering. Per sub-categorie zijn de **top 2–3 tools**
> volledig uitgewerkt (12-velden scorekaart); overige vondsten staan als *long tail* (naam + URL + 1 zin).
> Harde poort: **alléén open source** — open-core wordt beoordeeld op uitsluitend de community-editie,
> met expliciete vermelding van wat achter de betaalmuur zit. Licentie-vallen (BSL/SSPL/Elastic License 2.0/
> source-available) worden expliciet benoemd; OSI-goedkeuring is de norm. De SIEM-ruimte is bijzonder
> vervuild met open-core en niet-OSI-licenties — daar is extra zorgvuldig geflagd.
> EU-soevereiniteit is een zachte weging (zelf-hostbaarheid + dataresidentie); non-EU/SaaS-only mag, mét
> waarschuwing en lagere fit-score. Alle tool-claims zijn voorzien van ≥1 bron-URL. Peildatum: **juni 2026**.

> **Multi-functie-tools (let op voor dedup met andere CSF-documenten).** Verschillende tools hieronder raken
> meer dan alleen DETECT:
> - **Prowler / Steampipe** — ook GOVERN/IDENTIFY (compliance-mapping, NIST CSF-benchmarks).
> - **Wazuh** — ook PROTECT (FIM, SCA), RESPOND (active response), IDENTIFY (vulnerability-inventory).
> - **OpenCTI** — primair IDENTIFY (threat intelligence / TIP); hier opgenomen als detectie-voedingslaag.
> - **Suricata / Zeek / Falco** — ook RESPOND (Suricata IPS-blocking; Falco response-actions).
> - **Trivy / Grype / Dependency-Track** — ook IDENTIFY (SBOM, asset/dependency-inventory).

---

## 1. Security posture / CSPM

Het open-source CSPM-landschap kent één duidelijke koploper (**Prowler**, met expliciete NIST CSF 2.0-mapping)
en een sterke, SQL-gedreven alternatief (**Steampipe**). **ScubaGear** is relevant maar smal (alléén M365).
**CloudQuery** is in 2024 materieel uitgehold als open-source CSPM doordat de belangrijkste cloud-plugins
naar betaald zijn verplaatst — daarom long tail met expliciete waarschuwing.

### 1.1 Prowler — *primaire aanbeveling DETECT / CSPM*

1. **Naam + URL:** Prowler — https://github.com/prowler-cloud/prowler
2. **CSF-functie(s):** DETECT (primair: DE.CM continuous monitoring, configuratie-drift). Raakt sterk GOVERN/IDENTIFY (compliance-mapping NIST CSF 2.0, CIS, DORA, NIS2, ISO27001).
3. **Capability:** Multi-cloud security posture management & compliance-scanning (AWS, Azure, GCP, Kubernetes, M365).
4. **Omschrijving:** De facto open-source CSPM-standaard. 1000+ ingebouwde security-checks, gemapt op een groot aantal compliance-frameworks inclusief **NIST CSF 2.0** (DE.CM-controls per provider). Zelf-hostbare UI inbegrepen, plus CLI. Output in HTML/JSON/CSV. Zeer frequente release-cadans (meerdere per week). Op PyPI als `prowler-cloud`.
5. **Rijpheid:** **Hoog.** v5.28.1 (26 mei 2026). Grote, actieve community; $12,5M funding (april 2025) gericht op AI-gedreven security. Brede inzet in EU-publieke sector.
6. **Licentie:** Apache-2.0 (OSI-goedgekeurd, permissief). Geen BSL/SSPL. **Open-core:** continue monitoring (always-on), parallelle uitvoering, dashboards en de AI-assistent "Lighthouse" zitten in de betaalde Prowler Cloud / Enterprise. De volledige check-engine en alle frameworks zijn vrij.
7. **EU-soevereiniteit:** ✅ Uitstekend. OSS-versie volledig zelf-hostbaar, geen call-home, air-gap-capabel. Enterprise-tier biedt expliciet in-VPC / in-eigen-datacenter / air-gapped deployment. US-bedrijf, maar de tool zelf is schone Apache-2.0 zonder lock-in.
8. **Integreerbaarheid:** CLI + REST/UI. AWS Security Hub, S3, Jira, SIEM-export via JSON/CSV, Kubernetes, Docker, GitHub Actions.
9. **AI-native koppelbaarheid:** Ja (deels achter betaalmuur). **Prowler MCP Server** voor AI-toolintegratie bestaat; de "Lighthouse" AI-assistent is gated in Prowler Cloud.
10. **Stack/taal:** Python.
11. **Fit-score: 5/5.** Rijpste open-source CSPM, expliciete NIST CSF 2.0 DE.CM-mapping, multi-cloud, air-gappable, permissieve licentie. Beste keuze voor de DETECT-postuurlaag.
12. **Bronnen:**
    - https://github.com/prowler-cloud/prowler (release v5.28.1, mei 2026)
    - https://docs.prowler.com/projects/prowler-open-source/en/latest/
    - https://siliconangle.com/2025/04/02/prowler-raises-12-5m-advance-open-source-driven-cloud-security-platform/

---

### 1.2 Steampipe — *aanbeveling voor custom posture-queries (SQL)*

1. **Naam + URL:** Steampipe — https://github.com/turbot/steampipe
2. **CSF-functie(s):** DETECT (DE.AE, DE.CM via compliance-mods). Raakt GOVERN/IDENTIFY (NIST CSF v1.1 én v2.0-benchmarks).
3. **Capability:** SQL-gedreven cloud/SaaS-bevraging met live FDW; compliance-benchmarking via mods.
4. **Omschrijving:** Bevraagt cloud- en SaaS-API's als PostgreSQL-tabellen (Foreign Data Wrapper). 150+ plugins. Compliance-mods leveren kant-en-klare benchmarks: het `steampipe-mod-aws-compliance` bevat een volwaardige **NIST CSF v2.0**-benchmark inclusief DE.AE/DE.CM. Queries zijn SQL en volledig inspecteerbaar/aanpasbaar. Powerpipe levert dashboards, Flowpipe automation, Tailpipe log-ingestie.
5. **Rijpheid:** **Hoog.** v2.3.6 (feb 2026); v1.0-mijlpaal okt 2024. Actief commercieel gesteund door Turbot.
6. **Licentie:** **Split-licensing — let op.** CLI/FDW, Powerpipe, Flowpipe, Tailpipe = **AGPL-3.0** (OSI, sterk copyleft → juridische review bij embedding in product). Plugins én compliance-mods (incl. NIST CSF) = Apache-2.0 (permissief). Turbot biedt commerciële licentie om AGPL-restrictie weg te nemen.
7. **EU-soevereiniteit:** ✅ Goed. CLI + plugins draaien volledig lokaal, geen call-home. AGPL = code-beschikbaar (soevereiniteitsvriendelijk). ⚠️ Turbot Pipes (SaaS) heeft geen gedocumenteerde EU-regio — vermijd voor EU-dataresidentie van telemetrie.
8. **Integreerbaarheid:** PostgreSQL-native (FDW) → integreert in elke Postgres-stack, Grafana, Metabase. 150+ plugins (AWS/Azure/GCP/K8s/GitHub/M365). Flowpipe voor remediation-workflows.
9. **AI-native koppelbaarheid:** Deels. Geen native AI-assistent; het SQL-querymodel is uitstekend als databron voor AI-analyse.
10. **Stack/taal:** Go (CLI/FDW); SQL (queries/mods).
11. **Fit-score: 4/5.** Meest flexibele tool voor custom DETECT-queries met bestaande NIST CSF 2.0-benchmark; AGPL op de core verdient juridische review. Complementair aan Prowler (Prowler = kant-en-klare checks; Steampipe = maatwerk SQL).
12. **Bronnen:**
    - https://github.com/turbot/steampipe (release v2.3.6, feb 2026)
    - https://hub.powerpipe.io/mods/turbot/steampipe-mod-aws-compliance/dashboards/dashboard.nist_csf_v2
    - https://turbot.com/open-source

---

### 1.3 ScubaGear — *aanbeveling alléén bij Microsoft 365-scope*

1. **Naam + URL:** ScubaGear — https://github.com/cisagov/ScubaGear
2. **CSF-functie(s):** Primair IDENTIFY/PROTECT (secure baseline). Beperkte DETECT-dekking (config-assessment, niet continue eventdetectie).
3. **Capability:** Assessment van Microsoft 365-configuratie tegen CISA SCuBA-baselines.
4. **Omschrijving:** PowerShell + Open Policy Agent (OPA/Rego) die M365 (Entra ID, Exchange Online, SharePoint/OneDrive, Teams, Defender for Office 365, Power Platform) toetst tegen CISA-baselines. Output HTML/JSON/CSV. Gebouwd en onderhouden door **CISA** (US).
5. **Rijpheid:** **Hoog** binnen smalle scope. ~v1.8.x-lijn (2025); >30.000 downloads. Geen commerciële tier.
6. **Licentie:** **CC0-1.0** (publiek domein — maximaal permissief, geen attributie/copyleft). ⚠️ Sommige baseline-checks vereisen M365 E5/G5-licenties (Microsoft-afhankelijkheid, geen tool-paywall).
7. **EU-soevereiniteit:** ⚠️ Gemengd. Tool zelf draait lokaal tegen eigen tenant, stuurt zelf niets extern. Maar het toetst uitsluitend Microsoft 365 → de onderliggende infra valt onder US CLOUD Act ongeacht het assessment-tool. Soevereiniteitszorg ligt bij Microsoft, niet bij ScubaGear.
8. **Integreerbaarheid:** Standalone. JSON/HTML/CSV-output, te ingesten in SIEM/GRC. Geen native SIEM-integratie.
9. **AI-native koppelbaarheid:** Nee.
10. **Stack/taal:** PowerShell + OPA (Rego).
11. **Fit-score: 3/5.** Maximaal permissief en gezaghebbend (CISA), maar smal (M365-only) en zwakke native DETECT-dekking. Alleen relevant als M365 in scope is.
12. **Bronnen:**
    - https://github.com/cisagov/ScubaGear (LICENSE = CC0-1.0)
    - https://www.cisa.gov/resources-tools/services/secure-cloud-business-applications-scuba-project

---

### Long tail — CSPM / posture

- **CloudQuery** (https://github.com/cloudquery/cloudquery) — ETL/data-pipeline voor cloud-config naar SQL-DB;
  framework MPL-2.0, **maar de AWS/Azure/GCP-plugins zijn eind 2024 naar betaald verplaatst** → open-source
  CSPM-nut materieel uitgehold; geen ingebouwde NIST CSF-checks (DIY). ⚠️ Niet aanraden als open-source CSPM.
- **CloudSploit / Aqua cloudsploit** (https://github.com/aquasecurity/cloudsploit) — multi-cloud config-scanning;
  GPL-3.0; minder actief sinds Aqua's focus op commerciële platform; Prowler is het levendiger alternatief.
- **Kubescape** (https://github.com/kubescape/kubescape) — Kubernetes posture/compliance (NSA-CISA, CIS); Apache-2.0;
  CNCF incubating; sterke K8s-specifieke DE.CM-dekking, complementair aan Prowler.

---

## 2. Vulnerability management

Twee assen: **infrastructuur/netwerk-scanning** (Greenbone/OpenVAS) en **container/SBOM/dependency-scanning**
(Trivy, Grype, Dependency-Track, Nuclei). Voor EU-soevereine omgevingen zijn **Greenbone CE** (Duits) en
**OWASP Dependency-Track** de schoonste keuzes. ⚠️ **Trivy** kende een ernstig supply-chain-incident (maart 2026)
dat aanvullende controles vereist.

### 2.1 Greenbone Community Edition / OpenVAS — *primaire aanbeveling netwerk-VM*

1. **Naam + URL:** Greenbone CE / OpenVAS — https://github.com/greenbone/openvas-scanner
2. **CSF-functie(s):** DETECT (DE.CM vulnerability scanning). Raakt IDENTIFY (vulnerability-inventory).
3. **Capability:** Netwerk- en host-vulnerability-scanning (authenticated/unauthenticated), CVE-detectie, compliance-audit.
4. **Omschrijving:** Volwassen open-source vulnerability scanner (GVM-framework). Volledige scanner-engine, Community Feed met Vulnerability Tests (VTs), GMP/REST-API, `python-gvm`-library. Deploybaar via Docker Compose of Debian/Ubuntu-packages.
5. **Rijpheid:** **Hoog.** openvas-scanner 23.45.5 (20 mei 2026). Lange staat van dienst; Duitse leverancier (Greenbone AG, Osnabrück).
6. **Licentie:** **GPL-2.0-or-later** (copyleft, OSI). VTs in Community Feed eveneens GPL-2.0-or-later. **Open-core feed-wall:** in-house ontwikkelde VTs, compliance-audit-content (PCI-DSS, BSI), support/SLA en de Enterprise-appliance zitten in de **Enterprise Feed**. De Community Feed mist een deel van de nieuwste/proprietary VTs.
7. **EU-soevereiniteit:** ✅ Uitstekend. Duits bedrijf, volledig zelf-hostbaar, geen telemetrie, air-gapped mogelijk (lokale feed-mirror). Sterke NIS2/GDPR-fit; broncode auditbaar.
8. **Integreerbaarheid:** GMP (XML over TLS), `python-gvm`, `gvm-cli`/`gvm-tools`. REST-API in GOS/Enterprise.
9. **AI-native koppelbaarheid:** Nee (geen AI in OSS-stack).
10. **Stack/taal:** C (scanner), Python (tooling/API).
11. **Fit-score: 4/5.** Sterkste EU-soevereine netwerk-VM; copyleft + Duitse herkomst + auditbaar. Eén punt eraf door feed-wall (nieuwste/proprietary VTs achter betaalmuur) en relatief zware deployment.
12. **Bronnen:**
    - https://github.com/greenbone/openvas-scanner (release 23.45.5, mei 2026)
    - https://greenbone.github.io/docs/latest/background.html
    - https://forum.greenbone.net/t/differences-between-greenbones-commercial-and-community-products/8772

---

### 2.2 Trivy — *brede container/IaC/SBOM-scanner — mét supply-chain-waarschuwing*

1. **Naam + URL:** Trivy — https://github.com/aquasecurity/trivy
2. **CSF-functie(s):** DETECT (DE.CM). Raakt IDENTIFY (SBOM, asset/dependency-inventory).
3. **Capability:** All-in-one scanner: container images, filesystems, git-repos, K8s-clusters, IaC (Terraform/Helm), SBOM, secrets, licenties.
4. **Omschrijving:** Pure CLI-binary (Go, geen daemon/server). Breed inzetbaar in CI/CD en lokaal. Kubernetes-operator (`trivy-operator`, CRD-gebaseerd). Output SARIF/JSON/table.
5. **Rijpheid:** **Hoog.** v0.71.1 (15 juni 2026); zeer actief.
6. **Licentie:** **Apache-2.0** (OSI, permissief; bewust van AGPL-3.0 weggemigreerd om integratiedrempels te verlagen). Het commerciële Aqua Platform is een apart product, geen open-core van Trivy zelf — Trivy CLI kent geen feature-paywall.
7. **EU-soevereiniteit:** ⚠️ Goed CLI-profiel, **maar kritische supply-chain-waarschuwing.** In maart 2026 werd Aqua's GitHub gecompromitteerd: malafide `v0.69.4`-release + ge-force-pushte tags in `trivy-action`/`setup-trivy` ("TeamPCP Cloud Stealer", CI/CD-secrets-exfiltratie). De Europese Commissie behoorde tot 71+ getroffen instellingen (CERT-EU). Veilige versies: binary ≤ v0.69.3, trivy-action v0.35.0, setup-trivy v0.2.6; v0.71.x is schoon. Vereist hash-pinning + signature-verificatie bij EU-overheidsinzet.
8. **Integreerbaarheid:** CLI, GitHub Actions, `trivy-operator` (K8s), SARIF/JSON, AWS Security Hub, DefectDojo, SIEM-connectoren.
9. **AI-native koppelbaarheid:** Nee (geen native AI in OSS).
10. **Stack/taal:** Go.
11. **Fit-score: 4/5.** Breedste open-source scanner met schone Apache-2.0 en geen feature-paywall; één punt eraf wegens het supply-chain-incident dat expliciete keten-controles afdwingt.
12. **Bronnen:**
    - https://github.com/aquasecurity/trivy (release v0.71.1, juni 2026)
    - https://github.com/aquasecurity/trivy/security/advisories/GHSA-69fq-xp46-6x23
    - https://www.microsoft.com/en-us/security/blog/2026/03/24/detecting-investigating-defending-against-trivy-supply-chain-compromise/

---

### 2.3 OWASP Dependency-Track — *primaire aanbeveling SBOM/SCA — EU-soeverein*

1. **Naam + URL:** OWASP Dependency-Track — https://github.com/DependencyTrack/dependency-track
2. **CSF-functie(s):** DETECT (DE.CM continue componentmonitoring). Raakt IDENTIFY (SBOM/component-inventory), GOVERN (supply-chain-beleid).
3. **Capability:** Continue analyse van software-componenten (SCA) op basis van geïngeste SBOM's; alarmering bij nieuwe kwetsbaarheden in bekende componenten.
4. **Omschrijving:** Server-platform dat CycloneDX/SPDX-SBOM's ingest en componenten continu toetst tegen NVD, OSV, GitHub Advisories, Sonatype OSS Index. v5 ("Hyades") is een microservice-herontwerp: PostgreSQL-only, horizontaal schaalbaar, Kafka/Redpanda-bus, CEL-policy-engine, active/active HA. Door het **Nederlandse NCSC** genoemd als referentie-implementatie voor SBOM.
5. **Rijpheid:** **Hoog.** v5.0 GA (9 juni 2026). OWASP-gegoverneerd.
6. **Licentie:** **Apache-2.0** (OSI, permissief). Volledig open — geen enterprise-tier, geen paywall.
7. **EU-soevereiniteit:** ✅ Uitstekend. Volledig zelf-hostbaar, geen cloud-afhankelijkheid; PostgreSQL-only vereenvoudigt EU-publieke-sectorinzet. NCSC-NL-referentie.
8. **Integreerbaarheid:** Volledige REST-API; Kafka/Redpanda (v5); SBOM-ingest CycloneDX/SPDX; notificaties naar Slack/Teams/Email/Webhook/Jira; cdxgen-integratie; Helm-chart.
9. **AI-native koppelbaarheid:** Nee (geen native AI; cdxgen heeft losse AI-assist voor SBOM-generatie).
10. **Stack/taal:** Java (microservices); PostgreSQL.
11. **Fit-score: 5/5.** Schoonste EU-soevereine SBOM/SCA-keuze: Apache-2.0, OWASP-governance, NCSC-referentie, geen paywall. Beste keuze voor continue supply-chain-detectie.
12. **Bronnen:**
    - https://owasp.org/blog/2026/06/09/dependency-track-v5 (v5.0 GA, juni 2026)
    - https://github.com/DependencyTrack/dependency-track
    - https://github.com/DependencyTrack/hyades

---

### Long tail — vulnerability management

- **Grype** (https://github.com/anchore/grype) — Apache-2.0; container/SBOM-CVE-scanner (Anchore); v0.114.0 (juni 2026);
  CLI-only, geen account; pairt sterk met **Syft** (SBOM) → Grype → Dependency-Track-pipeline; US-bedrijf, OSS schoon.
- **Nuclei** (https://github.com/projectdiscovery/nuclei) — **MIT**; template-gebaseerde vuln-scanner; v3.8.0 (april 2026);
  12.000+ templates; **`-ai`-vlag** genereert templates uit natuurlijke taal (meest opvallende AI-feature in deze groep,
  maar AI-quota/managed scanning zit in US-gehoste PDCP-cloud — ⚠️ EU-dataresidentie); CLI volledig zelf-hostbaar.
- **Syft** (https://github.com/anchore/syft) — Apache-2.0; SBOM-generator (CycloneDX/SPDX); v1.44.0 (mei 2026);
  upstream-component van de Grype/Dependency-Track-keten; primair IDENTIFY maar voedt DETECT.

---

## 3. SIEM / monitoring

⚠️ **De meest licentie-vervuilde sub-categorie.** Alleen **Wazuh** (GPL-2.0) en **OpenSearch Security Analytics**
(Apache-2.0) zijn schoon OSI-open-source. **Elastic Security** is gedeeltelijk (core via AGPL-3.0 sinds aug 2024,
maar premium SIEM-features blijven ELv2/betaald). **Security Onion** is **niet** OSI-open-source (Elastic License 2.0,
source-available) → daarom long tail met expliciete flag. Netwerk-detectiesensoren (Suricata/Zeek) en runtime
(Falco) staan onder §4-aanpalend / long tail.

### 3.1 Wazuh — *primaire aanbeveling DETECT / SIEM*

1. **Naam + URL:** Wazuh — https://github.com/wazuh/wazuh
2. **CSF-functie(s):** DETECT (DE.CM, DE.AE log-/event-analyse). Raakt PROTECT (FIM, SCA), RESPOND (active response), IDENTIFY (vulnerability detection).
3. **Capability:** Open-source SIEM + XDR + HIDS: log-analyse, FIM, Security Configuration Assessment, vulnerability-detectie, MITRE ATT&CK-mapping, active response.
4. **Omschrijving:** Fork van OSSEC (2015), uitgegroeid tot volledig platform: agent + manager + indexer (op OpenSearch) + dashboard. 3000+ ingebouwde regels, MITRE ATT&CK ingebouwd. Geen community-vs-enterprise feature-split — alles is open.
5. **Rijpheid:** **Hoog.** v4.14.5 (23 april 2026); meerdere releases per kwartaal. Brede inzet in MKB en publieke sector.
6. **Licentie:** **GPL-2.0-only** (copyleft, OSI). ⚠️ Let op: sommige bronnen melden ten onrechte AGPLv3 — dat betreft een discussie (#16497) over de nieuwe "engine"-module, niet het hele platform; verifieer tegen de LICENSE-file. Wazuh Inc. verkoopt alléén support-contracten, geen feature-paywall.
7. **EU-soevereiniteit:** ✅ Sterk. GPL-2.0, volledig zelf-hostbaar, geen call-home, geen US-cloud-afhankelijkheid. US-bedrijf, maar de software legt geen soevereiniteitsbeperking op. Veel gebruikt in EU-publieke sector om precies deze reden.
8. **Integreerbaarheid:** MISP (officieel, okt 2025), TheHive, Sigma (via pipeline), ESET (officieel apr 2025), OpenCTI, VirusTotal, Slack, PagerDuty, Jira (community). OpenSearch als indexer (native).
9. **AI-native koppelbaarheid:** Deels (via integratie). Geen ingebouwde ML/AI in v4.x; AI via externe modellen (OpenAI/Ollama voor soeverein-lokaal) of de onderliggende OpenSearch ML-engine. Officiële blog documenteert AI-augmented threat-hunting.
10. **Stack/taal:** C (engine), Python/JS (tooling/dashboard); OpenSearch-indexer.
11. **Fit-score: 5/5.** Schoonste en meest complete open-source SIEM voor DETECT: GPL-2.0 zonder paywall, sterke threat-intel-integratie, actief, EU-zelf-hostbaar. AI vereist externe koppeling (kan soeverein via Ollama).
12. **Bronnen:**
    - https://github.com/wazuh/wazuh (release 4.14.x)
    - https://documentation.wazuh.com/current/release-notes/release-4-14-2.html
    - https://www.misp-project.org/2025/10/06/wazuh-integration.html/

---

### 3.2 OpenSearch Security Analytics — *aanbeveling soevereine, schone Apache-stack*

1. **Naam + URL:** OpenSearch Security Analytics — https://opensearch.org/platform/security-analytics/ · https://github.com/opensearch-project/OpenSearch
2. **CSF-functie(s):** DETECT (DE.AE, DE.CM: log-correlatie, alerting, Sigma-detectie, anomaly-detectie).
3. **Capability:** SIEM-plugin op de OpenSearch-zoek/analyse-engine: detectors uit Sigma-regels, alert-management, MITRE ATT&CK-mapping, anomaly-detectie via ML-plugin.
4. **Omschrijving:** Native plugin in elke OpenSearch-distributie. Gevorkt van Elasticsearch 7.10 (laatste Apache-2.0-versie) door AWS in 2021. Sinds 2024-2025 onder **Linux Foundation**-governance.
5. **Rijpheid:** **Hoog-middel.** OpenSearch 3.x-lijn (3.1/3.2/3.3) uitgebracht 2025-2026; 2.x stabiel. SIEM-featurediepte is geringer dan Wazuh/Elastic out-of-the-box maar groeit.
6. **Licentie:** **Apache-2.0** (OSI, permissief) — schoon en ondubbelzinnig. Geen premium-tier voor de core SIEM-functionaliteit; AWS OpenSearch Service is alleen een betaalde hosting, geen feature-gate.
7. **EU-soevereiniteit:** ✅ Sterkste profiel in deze categorie. Apache-2.0 + Linux Foundation-governance (geen enkele US-vendor controleert proprietary de roadmap). Volledig zelf-hostbaar binnen EU-infra.
8. **Integreerbaarheid:** Wazuh gebruikt OpenSearch als indexer; AWS-securitydiensten (GuardDuty/CloudTrail/Security Hub) native; Logstash/Fluentd/OpenTelemetry; Grafana-datasource.
9. **AI-native koppelbaarheid:** Ja (deels, gratis). OpenSearch 3.2 introduceerde **agentic AI** en hybride vector/keyword-search; ML Commons-plugin (Apache-2.0) voor model-integratie en anomaly-detectie; neural/semantic search.
10. **Stack/taal:** Java; PPL/query-DSL.
11. **Fit-score: 4/5.** Beste soevereiniteitsprofiel (Apache-2.0 + LF-governance) met gratis agentic-AI; één punt eraf wegens geringere kant-en-klare SIEM-featurediepte dan Wazuh.
12. **Bronnen:**
    - https://opensearch.org/platform/security-analytics/
    - https://github.com/opensearch-project/OpenSearch
    - https://www.instaclustr.com/education/opensearch/complete-guide-to-opensearch-in-2025/

---

### 3.3 Elastic Security (ELK SIEM) — *gedeeltelijk open source — lees licentie zorgvuldig*

1. **Naam + URL:** Elastic Security — https://www.elastic.co/security/siem · https://github.com/elastic/elasticsearch
2. **CSF-functie(s):** DETECT (DE.AE, DE.CM). Raakt RESPOND (automated response — betaald).
3. **Capability:** SIEM op de Elastic Stack: log-ingest, detectie-engine (1300+ prebuilt rules), ML-anomaly-detectie, AI Assistant — de geavanceerde lagen zijn betaald.
4. **Omschrijving:** Volwassen, breed ecosysteem (ECS, 300+ integraties via Fleet). De detection-rules-repo (https://github.com/elastic/detection-rules) is Apache-2.0 maar wordt niet auto-geüpdatet in de free tier.
5. **Rijpheid:** **Hoog.** Elasticsearch/Kibana 8.x én 9.x (9.x in 2025).
6. **Licentie:** **Tri-license: SSPL-1.0 / Elastic License 2.0 / AGPL-3.0** (AGPL-optie toegevoegd aug 2024 → core is legitiem OSI via AGPL). ⚠️ **Maar:** AGPL dekt alleen de core search-engine; **premium SIEM-features (ML-anomaly, behavioral analytics, AI Assistant, automated response) blijven onder ELv2/abonnement.** Behandel Elastic SIEM **niet** als volledig open source voor procurement/compliance.
7. **EU-soevereiniteit:** ⚠️ Middel. US-bedrijf (NYSE: ESTC). Zelf-hosten op EU-infra mogelijk (AGPL = geen license-key-enforcement op de core), maar Elastic Cloud valt onder US-verwerkersovereenkomsten; premium-features blijven vendor-gecontroleerd.
8. **Integreerbaarheid:** 300+ integraties via Elastic Agent/Fleet; AWS/Azure/GCP native; MISP/TAXII; SOAR.
9. **AI-native koppelbaarheid:** Ja, maar **betaald.** AI Assistant for Security (Enterprise) voor alert-triage; ML-anomaly-jobs (Platinum+). Plain-English → ES|QL detectieregel-generatie aangekondigd.
10. **Stack/taal:** Java (Elasticsearch), TypeScript (Kibana).
11. **Fit-score: 3/5.** Krachtig en volwassen, maar de feitelijk bruikbare SIEM-/AI-capaciteiten zitten achter de ELv2-betaalmuur; "open source"-claim is misleidend voor de securitylaag. Free/AGPL-tier is functioneel beperkt.
12. **Bronnen:**
    - https://www.elastic.co/blog/elasticsearch-is-open-source-again
    - https://www.elastic.co/pricing/faq/licensing
    - https://www.comparitech.com/net-admin/elastic-siem-review-alternatives/

---

### Long tail — SIEM / monitoring & sensoren

- **Security Onion** (https://github.com/Security-Onion-Solutions/securityonion) — ⚠️ **niet OSI-open-source:**
  Elastic License 2.0 (source-available; verbiedt hosted-service en license-key-bypass). Sterke geïntegreerde
  NSM+SIEM+case-platform (Suricata/Zeek/osquery/CyberChef), maar "Onion AI Assistant" is Pro/betaald; Wazuh in
  2.4.x vervangen door Elastic Agent (verdiept ELv2-afhankelijkheid). v2.4.200 (dec 2025); SO 3.0 gepland 2026.
- **Suricata** (https://github.com/OISF/suricata) — **GPL-2.0** (OISF, community-non-profit, EU-vriendelijke governance);
  v8.0.2 (nov 2025); netwerk-IDS/IPS + NSM, deep packet inspection, EVE-JSON; raakt RESPOND (IPS-blocking);
  pairt met Wazuh/OpenSearch voor SIEM-integratie.
- **Zeek** (https://github.com/zeek/zeek) — **BSD** (meest permissief); v8.0.4 (nov 2025); network security monitor /
  protocol-analyse, genereert rijke metadata voor ML-pipelines; complementair aan Suricata (Zeek = analytics, Suricata = alerting).
- **Falco** (https://github.com/falcosecurity/falco) — **Apache-2.0**; CNCF graduated (feb 2024); v0.43.0 (jan 2026);
  cloud-native runtime/syscall-detectie + K8s-audit; vult de runtime-detectiegap die klassieke SIEM-agents missen.
- **OSSEC** (https://github.com/ossec/ossec-hids) — GPL-2.0; voorganger van Wazuh; effectief in maintenance
  (3.8.0, jan 2021); alleen relevant voor zeer lichte legacy-omgevingen — nieuw: kies Wazuh.

---

## 4. Detection-as-code / detectie-engineering

De ruggengraat hier is **Sigma** (vendor-neutraal regelformaat). **YARA/YARA-X** dekt malware-patroonmatching;
**Hayabusa/Chainsaw** brengen Sigma naar Windows-EVTX-forensiek; **OpenCTI** voedt detecties met threat intel
(primair IDENTIFY). **Elastic detection-rules** is source-available (ELv2) → long tail met flag.

### 4.1 Sigma (SigmaHQ) — *primaire aanbeveling detection-as-code*

1. **Naam + URL:** Sigma — https://github.com/SigmaHQ/sigma
2. **CSF-functie(s):** DETECT (DE.AE, DE.CM: vendor-neutrale detectielogica).
3. **Capability:** Generiek, leesbaar YAML-regelformaat voor log-gebaseerde detectie, converteerbaar naar vrijwel elke SIEM-query-taal.
4. **Omschrijving:** De facto open standaard voor detectieregels. 3000+ community-regels, alle gemapt op MITRE ATT&CK (Windows/Linux/AWS/Azure/M365/Okta/netwerk). `pySigma`-backends compileren naar Splunk SPL, Microsoft KQL/Sentinel, Elastic EQL, QRadar, Chronicle YARA-L, OpenSearch, Wazuh. Voorkomt vendor-lock-in van detectielogica — belangrijk voor EU-soevereiniteit.
5. **Rijpheid:** **Hoog.** Regelpakket `r2026-01-01`; doorlopende releases; grote actieve community.
6. **Licentie:** **Detection Rule License (DRL 1.1)** voor de regels; tooling LGPL-2.1/3.0 en MIT. ⚠️ DRL is permissief en volledig open in de praktijk maar **niet OSI-gecertificeerd** in klassieke zin (purpose-built voor detectielogica, vereist attributie).
7. **EU-soevereiniteit:** ✅ Uitstekend. Puur tekstformaat + lokale tooling; geen runtime-afhankelijkheid; vendor-neutraal = geen lock-in.
8. **Integreerbaarheid:** Vrijwel alle SIEM's via pySigma-backends; Hayabusa/Chainsaw consumeren Sigma native.
9. **AI-native koppelbaarheid:** Deels. Geen native AI in SigmaHQ; wél geconsumeerd door AI-tools (Sentinel/Elastic genereren Sigma uit natuurlijke taal). Het standaardformaat is een ideale AI-output/-input-laag.
10. **Stack/taal:** YAML (regels), Python (pySigma-tooling).
11. **Fit-score: 5/5.** Fundament voor detection-as-code: vendor-neutraal, lock-in-vrij, EU-soeverein, breed geadopteerd. DRL-licentie verdient een notitie maar is in de praktijk vrij.
12. **Bronnen:**
    - https://github.com/SigmaHQ/sigma (release r2026-01-01)
    - https://github.com/SigmaHQ/Detection-Rule-License
    - https://sigmahq.io/docs/guide/about.html

---

### 4.2 YARA-X — *aanbeveling malware-patroonmatching*

1. **Naam + URL:** YARA-X — https://github.com/VirusTotal/yara-x (klassiek: https://github.com/VirusTotal/yara)
2. **CSF-functie(s):** DETECT (DE.CM: malware-/IOC-detectie in files, processen, geheugen).
3. **Capability:** Patroonmatching-"swiss knife" voor identificatie/classificatie van malware via string-, byte-, regex- of metadata-condities.
4. **Omschrijving:** YARA-X is de Rust-herschrijving (memory-safe, sneller, betere errors, decoupled parser/scanner) en de actieve opvolger van klassiek YARA (nu maintenance). VirusTotal gebruikt YARA-X in productie (Livehunt/Retrohunt). Python/Rust/Go-bindings.
5. **Rijpheid:** **Hoog.** YARA-X v1.0.0 (juni 2025, eerste stabiele); klassiek YARA v4.5.5 (okt 2025, maintenance).
6. **Licentie:** **BSD-3-Clause** (OSI, permissief — schoon).
7. **EU-soevereiniteit:** ✅ Uitstekend. Volledig lokaal, geen runtime-afhankelijkheid, permissief.
8. **Integreerbaarheid:** Wazuh (endpoint-detectie), VirusTotal, MalwareBazaar, OpenCTI-enrichment, MISP, sandbox-platforms, Velociraptor; Rust/Python/Go-bindings.
9. **AI-native koppelbaarheid:** Nee native (wél vaak output van AI-gedreven malware-analyse-pipelines).
10. **Stack/taal:** Rust (YARA-X); C (klassiek).
11. **Fit-score: 5/5.** De standaard voor malware-patroonmatching; schone BSD-licentie; actieve Rust-opvolger; brede integratie met Wazuh/MISP/OpenCTI.
12. **Bronnen:**
    - https://github.com/VirusTotal/yara-x (v1.0.0, juni 2025)
    - https://blog.virustotal.com/2025/06/yara-x-100-stable-release-and-its.html
    - https://github.com/inquest/awesome-yara

---

### 4.3 OpenCTI — *aanbeveling threat-intelligence-voedingslaag*

1. **Naam + URL:** OpenCTI — https://github.com/OpenCTI-Platform/opencti
2. **CSF-functie(s):** Primair IDENTIFY (TIP). Voedt DETECT (DE.AE: IOC's/TTP's naar SIEM); raakt RESPOND.
3. **Capability:** Threat-intelligence-platform: opslaan/correleren/visualiseren van indicatoren, TTP's, actoren, campagnes, kwetsbaarheden.
4. **Omschrijving:** STIX2-kennismodel + GraphQL-API. Modulaire connector-architectuur (300+ integraties: MISP, TheHive, Shodan, VirusTotal, MITRE ATT&CK, TAXII). Oorspronkelijk co-ontwikkeld met **ANSSI** (FR) en CERT-EU; commercieel beheerd door **Filigran** (FR/EU).
5. **Rijpheid:** **Hoog.** v7.260609.0 (9 juni 2026); LTS-lijn sinds feb 2026.
6. **Licentie:** **Apache-2.0** (Community Edition, OSI). **Open-core:** Enterprise Edition (proprietary Filigran-licentie) bevat de "Ask AI"/Ariane-AI-analyse, agentic AI en geavanceerde playbooks.
7. **EU-soevereiniteit:** ✅ Uitstekend. EU-bedrijf (Filigran, FR), ANSSI/CERT-EU-oorsprong, volledig zelf-hostbaar.
8. **Integreerbaarheid:** GraphQL-API; 300+ connectoren; voedt SIEM/SOAR (Splunk/Elastic/Sentinel) downstream als TIP-laag.
9. **AI-native koppelbaarheid:** Ja (deels betaald). `ImportDocumentAI`-connector (PDF→STIX) en "Ask AI"/Ariane-AI-analyse — grotendeels Enterprise Edition.
10. **Stack/taal:** JavaScript/TypeScript (Node.js), GraphQL; Python-connectoren.
11. **Fit-score: 4/5.** Sterkste open-source TIP en uitstekende EU-soevereiniteit (FR-oorsprong); voedt DETECT met intel. Punt eraf omdat de AI-laag grotendeels achter EE-paywall zit; primair een IDENTIFY-tool.
12. **Bronnen:**
    - https://github.com/OpenCTI-Platform/opencti (v7.260609.0, juni 2026)
    - https://filigran.io/blog/opencti-v7/
    - https://docs.opencti.io/latest/reference/artificial-intelligence/

---

### Long tail — detection-as-code

- **Elastic detection-rules** (https://github.com/elastic/detection-rules) — ⚠️ **Elastic License v2 (source-available,
  niet OSI);** 1300+ prebuilt rules (ES|QL/KQL/EQL); AI rule-generation uit plain-English (mei 2026) en AI-migratie
  vanaf QRadar — maar gebonden aan Elastic Stack en niet vrij herdistribueerbaar. Sommige geïmporteerde regels
  behouden Apache-2.0/MIT.
- **Hayabusa** (https://github.com/Yamato-Security/hayabusa) — **GPL-3.0**; v3.5.0 (aug 2025); Rust; Sigma-gebaseerde
  Windows-EVTX-timeline/threat-hunting (grootste native Sigma-support van OSS Windows-log-analyzers); JP-community;
  geen native AI.
- **Chainsaw** (https://github.com/WithSecureLabs/chainsaw) — **GPL-3.0**; v2.14.x; Rust; snelle DFIR-triage van Windows-
  forensische artefacten (EVTX/MFT/Shimcache/SRUM/ESE) via Sigma (tau-engine); EU-oorsprong (WithSecure, FI).
- **YARA klassiek** (https://github.com/VirusTotal/yara) — BSD-3-Clause; v4.5.5 (okt 2025, maintenance); kies YARA-X voor nieuw werk.

---

## Niet-gedekt / gaps

- **NDR/network detection als losse productlaag** — Suricata + Zeek dekken de sensoren, maar er is geen rijp,
  volledig open-source NDR-*platform* (correlatie + UI + ML) dat met commerciële NDR concurreert; integratie via
  Wazuh/OpenSearch blijft handwerk.
- **UEBA / gedragsanalyse** — geen schone open-source UEBA-tool. ML-anomaly zit ofwel betaald (Elastic Platinum+)
  ofwel als losse bouwsteen (OpenSearch ML Commons, Wazuh + extern model). Een kant-en-klare open UEBA ontbreekt.
- **SOAR / response-orkestratie** — valt grotendeels onder RESPOND, maar de detect→respond-koppeling (TheHive/Cortex,
  Shuffle, Tines-OSS-achtig) is fragmentarisch; TheHive's recente licentie-/edition-verschuivingen verdienen aparte toetsing.
- **AI-native open-source SIEM** — bestaat (juni 2026) niet als volwassen product. Alle AI-native SIEM's (bv. Databricks
  Lakewatch, mrt 2026) zijn proprietary/SaaS. De soevereine route is een *samenstelling*: Wazuh/OpenSearch + lokaal
  LLM (Ollama + open weights) + Sigma — geen out-of-the-box product.
- **Cloud-/identity-threat-detection (ITDR)** — Entra/Okta-gedragsdetectie is dun in OSS; Sigma-regels bestaan, maar
  een dedicated open ITDR-engine ontbreekt; ScubaGear dekt alleen statische M365-config, niet runtime-eventdetectie.
- **macOS-endpoint-detectie** — sterk Windows-bias (Hayabusa/Chainsaw/Sysmon-Sigma); volwassen open-source macOS-EDR
  (buiten osquery/Falco-raakvlakken) ontbreekt grotendeels.
- **Licentie-attentiepunten (samengevat):** Elastic Security & Security Onion = niet/gedeeltelijk OSI (ELv2/SSPL);
  CloudQuery cloud-plugins = betaald; Sigma DRL = open maar niet OSI-gecertificeerd; Steampipe core = AGPL-3.0;
  Trivy = let op supply-chain-incident maart 2026 (hash-pinning verplicht).
