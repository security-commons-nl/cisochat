# RECOVER — open-source tooling landscape (NIST CSF 2.0)

> **Scope.** Dit document inventariseert open-source tooling voor de NIST CSF 2.0-functie **RECOVER** (RC)
> ten behoeve van een generieke, framework-agnostische vCISO-blueprint. De functie RECOVER omvat
> incidentherstel & communicatie (RC.CO), backup & herstel-orchestratie, bedrijfscontinuïteit (BCM/ISO 22301),
> disaster-recovery-planning & -testing, en post-incident-review / lessons-learned / blameless postmortems.
> Per sub-categorie zijn de **top 2–3 tools** volledig uitgewerkt (12-velden scorekaart); overige vondsten
> staan als *long tail* (naam + URL + 1 zin).
> Harde poort: **alléén open source** — open-core wordt beoordeeld op uitsluitend de community-editie,
> met expliciete vermelding van wat achter de betaalmuur zit. Licentie-vallen (proprietary "community"-
> tiers, custom licenties, source-available) worden expliciet benoemd; OSI-goedkeuring is de norm.
> EU-soevereiniteit is een zachte weging (zelf-hostbaarheid + dataresidentie).
> Alle tool-claims zijn voorzien van ≥1 bron-URL. Peildatum onderzoek: **juni 2026**.

> ⚠️ **Structureel gap-signaal: RECOVER is de dunste CSF-functie qua toegewijde OSS.**
> Backup-tools bestaan volop. Maar voor de *governance- en proceskant* van RECOVER — dedicated BCM-/ISO 22301-
> managementsoftware (BIA-workflows, continuïteitsplannen, oefening-logging), DR-planningtools en
> postmortem-managementplatformen — bestaat nauwelijks gespecialiseerde open-source tooling. Dit is een
> bekende marktfout: commerciële aanbieders (Fusion, Riskonnect, Everbridge, Cutover) domineren dit segment.
> De "Niet-gedekt / gaps"-paragraaf onderaan documenteert dit uitgebreid. Eramba (lang als open-source GRC
> geciteerd) is **buiten de harde poort** geplaatst: de community-editie gebruikt een **custom proprietary
> licentie** die herdistributie verbiedt en de GitHub-repo is privé. Zie toelichting bij §2.

---

## 1. Backup & herstel-orchestratie

De dichtstbevolkte sub-categorie van RECOVER in OSS-land. Deduplicerende, versleutelde backup-tools
(restic, BorgBackup) zijn de de facto standaard voor moderne file-level backups. Bacula/Bareos zijn de
enterprise-grade netwerk-backup-suites. Velero is de CNCF-standaard voor Kubernetes. Duplicati vult de
grafische/Windows-kant.

### 1.1 restic — *primaire aanbeveling: file-level backup*

1. **Naam + URL:** restic — https://restic.net/ · https://github.com/restic/restic
2. **CSF-functie(s):** RECOVER (primair: backup & herstel). Raakt PROTECT (data-integriteit via hash-verificatie).
3. **Capability:** Deduplicerende, versleutelde file-level backup naar meerdere backends (lokaal, SSH/SFTP,
   S3-compatible, Azure, GCS, Backblaze B2, rclone-backends).
4. **Omschrijving:** Enkelvoudig statisch Go-binary (geen server-component vereist) met content-defined
   chunking voor deduplicatie, AES-256-CTR versleuteling en geïntegreerde integriteitsverificatie van elke
   restore. Ondersteunt alle grote OS'en (Linux, macOS, Windows, BSD). Breed ingezet als bouwsteen in
   backup-pipelines; grote ecosysteem van GUI-wrappers (Resticara, Resticker, Vorta) en orchestratie-
   wrappers (autorestic). 34.000 GitHub-sterren (juni 2026).
5. **Rijpheid:** **Zeer hoog.** Productie-volwassen project, actief ontwikkeld, 419 contributors, 31+ releases.
   Breed gedocumenteerd en gebruikt in enterprise-omgevingen.
6. **Licentie:** **BSD 2-Clause** (OSI-goedgekeurd, permissief). Geen open-core, geen betaalmuur.
7. **EU-soevereiniteit:** ✅ On-prem of op eigen object-storage zelf-hostbaar. Geen verplichte externe
   cloud-afhankelijkheid. Volledig in eigen beheer te draaien.
8. **Integreerbaarheid:** CLI-first; volledig scriptbaar. JSON-output (machine-readable). REST-achtige
   operator-interface via diverse wrappers. Integreert met cron, Ansible, Kubernetes CronJobs.
9. **AI-native koppelbaarheid:** Nee (geen native MCP/API-server). Indirect via CLI-automatisering.
10. **Stack/taal:** Go (single binary). Geen externe runtime-afhankelijkheid.
11. **Fit-score: 5/5.** Gouden standaard voor encrypted deduplicating file backup; permissieve licentie;
    actief onderhouden; cross-platform; uitstekende EU-fit.
12. **Bronnen:**
    - https://github.com/restic/restic (BSD-2-Clause badge, 34k stars geverifieerd jun 2026)
    - https://en.wikipedia.org/wiki/Restic
    - https://restic.net/
    - https://servercrate.net/restic-vs-duplicacy/ (licentie-verificatie)

---

### 1.2 BorgBackup — *aanbeveling: deduplicatie + encryptie, Linux/Unix-omgevingen*

1. **Naam + URL:** BorgBackup — https://borgbackup.org/ · https://github.com/borgbackup/borg
2. **CSF-functie(s):** RECOVER (backup & herstel). Raakt PROTECT (data-integriteit).
3. **Capability:** Deduplicerend, versleuteld backup-archief met FUSE-mountbaar browse-systeem en SSH-transport.
4. **Omschrijving:** Content-defined chunking op chunk-niveau (variabele blokgrootte) voor hoogste
   deduplicatieverhouding; AES-OCB of ChaCha20-Poly1305 versleuteling; meerdere compressie-algoritmen
   (lz4, zstd, zlib, lzma). Benchmark-voordeel t.o.v. restic bij grote datasets (180–220 MB/s vs. 120–160
   MB/s) en betere compressie (zstd, 30–50% additioneel boven deduplicatie). FUSE-mount maakt archief
   browsebaar als bestandssysteem. Borgmatic (wrapper) voegt YAML-configuratie, pre/post-hooks en
   monitoring-integratie toe. 13.400 GitHub-sterren; laatste release v1.4.4 (19 maart 2026).
5. **Rijpheid:** **Zeer hoog.** Al actief since 2015; "The Borg Collective" community; 123 releases; brede
   Linux-distributie-packages. Borg 2.0 beta in ontwikkeling.
6. **Licentie:** **BSD 3-Clause** (OSI-goedgekeurd, permissief). Volledig open source.
7. **EU-soevereiniteit:** ✅ SSH-gebaseerde off-site backup naar eigen server. Geen externe cloud vereist.
8. **Integreerbaarheid:** CLI + REST via borgmatic-wrapper. Prometheus-metrics via borgmatic-integratie.
   GUI: Vorta (cross-platform).
9. **AI-native koppelbaarheid:** Nee (geen native MCP/API).
10. **Stack/taal:** Python (86.9%) + Cython/C voor performance-kritische paden. Enkele binary beschikbaar.
11. **Fit-score: 4/5.** Topkeuze voor grote Linux/Unix-omgevingen met deduplicatie-prioriteit; iets
    complexere multi-OS setup dan restic (Windows: experimenteel via WSL/Cygwin).
12. **Bronnen:**
    - https://github.com/borgbackup/borg (BSD-3-Clause, 13.4k stars, release v1.4.4 geverifieerd)
    - https://borgbackup.org/
    - https://www.temok.com/blog/restic-vs-borg (performance-benchmark)
    - https://borgbackup.readthedocs.io/en/stable/introduction.html

---

### 1.3 Velero — *aanbeveling: Kubernetes cluster backup & DR*

1. **Naam + URL:** Velero — https://velero.io/ · https://github.com/velero-io/velero
2. **CSF-functie(s):** RECOVER (primair: K8s backup & disaster recovery, cluster-migratie). Raakt PROTECT
   (data-bescherming persistent volumes).
3. **Capability:** Kubernetes-native backup, restore, disaster recovery en cluster-migratie (resources + PVs).
4. **Omschrijving:** CNCF Sandbox-project (gedoneerd door Broadcom, geaccepteerd door TOC op KubeCon EU 2026;
   maintainers van Broadcom, Red Hat en Microsoft). Maakt on-demand en geplande cluster-snapshots, inclusief
   persistent volumes. Ondersteunt cross-cluster migratie en productie-naar-dev-replicatie. Integreert met
   populaire object-stores (S3, GCS, Azure Blob). Pluginmodel voor volume-snapshots (CSI-snapshots, vendor-
   plugins). Actief onderhouden: v1.18.1 (19 mei 2026); 10.100 GitHub-sterren.
5. **Rijpheid:** **Hoog.** Oorsprong bij Heptio (K8s-mede-oprichters), via VMware, nu CNCF Sandbox. Breed
   ingezet in productie. 172 releases, actieve PR-stroom.
6. **Licentie:** **Apache-2.0** (OSI-goedgekeurd, permissief). Volledig open source — geen tiers.
7. **EU-soevereiniteit:** ✅ Zelf-hostbaar in eigen K8s-cluster met eigen object-storage (MinIO on-prem).
   Geen SaaS-afhankelijkheid.
8. **Integreerbaarheid:** Kubernetes CRD + CLI (velero). REST/Watch API via K8s. Hooks voor pre/post-backup-
   scripts. Plugin-ecosystem voor storage-providers.
9. **AI-native koppelbaarheid:** Deels. Geen native MCP-server, maar K8s-API + CLI maken automatisering
   in LLM-pipelines goed mogelijk.
10. **Stack/taal:** Go (98%). Kubernetes-native (CRDs, operators).
11. **Fit-score: 5/5 voor K8s-omgevingen.** De standaard OSS-keuze voor K8s backup & DR; CNCF-governance;
    permissieve licentie; actief onderhouden. Buiten K8s: niet van toepassing.
12. **Bronnen:**
    - https://github.com/velero-io/velero (Apache-2.0, 10.1k stars, v1.18.1 geverifieerd)
    - https://thenewstack.io/broadcom-velero-cncf-kubernetes/ (CNCF Sandbox donatie)
    - https://www.techzine.eu/news/infrastructure/139783/broadcom-ships-vks-3-6-and-moves-velero-to-cncf-sandbox/
    - https://velero.io/

---

### Long tail — Backup & herstel

- **Bareos** (https://github.com/bareos/bareos, AGPLv3, 1.2k stars) — Enterprise-grade netwerk-backup-suite, volledig open-source fork van Bacula 5.2 met Hyper-V/Proxmox-plugins en Windows DR-imaging (Barri); v25.0.3 april 2026.
- **Bacula** (https://www.bacula.org/, AGPLv3 dual-licensed) — De veteraan-enterprise-backup-suite voor complexe heterogene netwerken; open-core: Bacula Systems verkoopt Enterprise-editie; AGPLv3 community-editie functioneel maar minder features dan Enterprise.
- **Duplicati** (https://github.com/duplicati/duplicati, MIT) — GUI-gedreven, cross-platform (Windows/Linux/macOS) versleutelde cloud-backup-client; 30+ cloud-backends; MIT-licentie (gewijzigd van LGPL in maart 2024); stabiele release 2.1.0.5 (maart 2025).
- **Amanda** (https://www.amanda.org/) — Netwerk-breed multi-server backup-systeem voor disk, tape en cloud; volwassen maar trager ontwikkeltempo.
- **Duplicity** (https://duplicity.us/) — CLI-tool voor versleutelde incrementele backups naar S3/GDrive/FTP; python-gebaseerd; stabiel maar minder actief dan restic/borg.
- **Rclone** (https://rclone.org/) — Cloud-storage synchronisatie-tool (niet primair backup), maar breed ingezet als backend voor backup-pipelines; ondersteunt 70+ providers.
- **Clonezilla** (https://sourceforge.net/projects/clonezilla/) — Disk-imaging en partitie-cloning tool voor bare-metal DR-herstel; geen netwerk-backup maar snelle systeem-restore.
- **DRBD** (https://linbit.com/drbd/) — Open-source distributed replicated block device voor Linux; synchrone HA-replicatie lokaal + asynchrone DR-replicatie off-site; ingebakken in Linux-kernel; Linbit beheert ook commerciële LINSTOR-laag bovenop.

---

## 2. BCM / bedrijfscontinuïteit (ISO 22301, BIA, continuïteitsplannen)

> ⚠️ **Licentie-bevinding: Eramba valt buiten de harde poort.**
> Eramba wordt in veel bronnen als "open source GRC" geciteerd, maar de community-editie gebruikt een
> **custom proprietary licentie** die herdistributie verbiedt. De GitHub-repository is privé. De broncode
> is ingebakken in Docker-images maar niet vrijelijk opnieuw te distribueren. De maintainer heeft dit
> expliciet bevestigd op het eigen forum: *"The license permits users to adapt the code for their own use
> only, but prohibits repackaging and redistributing modified versions."* Eramba is daarmee **source-
> available, niet open source** (OSI-definitie). Eramba wordt hieronder als long-tail-notitie opgenomen
> met expliciete licentie-waarschuwing.

Dit is de sub-categorie met de meest uitgesproken OSS-schaarste. Specifieke BCM-software (ISO 22301-
ondersteuning, BIA-workflows, continuïteitsplan-lifecycle, oefening-logging) bestaat in de OSS-wereld
bijna niet als dedicated tool. De enige serieuze kandidaat is **CISO Assistant**, dat ISO 22301 als
framework ondersteunt als onderdeel van een bredere GRC-scope.

### 2.1 CISO Assistant (intuitem) — *enige aanbeveling BCM/GRC met ISO 22301-ondersteuning*

1. **Naam + URL:** CISO Assistant — https://github.com/intuitem/ciso-assistant-community · https://intuitem.com/
2. **CSF-functie(s):** Primair GOVERN (GRC, risk, compliance). Raakt RECOVER via ISO 22301-framework-ondersteuning
   en BIA-module. Multi-CSF-functie tool.
3. **Capability:** Geïntegreerde GRC-suite met compliance-/audit-management, risk management, BIA en 150+
   framework-bibliotheken waaronder ISO 22301:2019.
4. **Omschrijving:** Frans open-source GRC-platform (intuitem) met de breedste framework-dekking van alle
   OSS-GRC-tools (150+ frameworks, waaronder ISO 22301, NIST CSF 2.0, NIS2, DORA, ISO 27001, SOC2, GDPR).
   BIA-module is aanwezig: gebruikers kunnen BIA-assessments uitvoeren gekoppeld aan assets en acties voor
   cyberweerbaarheids-structurering. ISO 22301:2019-outline is direct als framework beschikbaar. v3.18.1
   uitgebracht 15 juni 2026; 4.100 GitHub-sterren. Python (Django) backend, Svelte frontend; PostgreSQL
   of SQLite.
5. **Rijpheid:** **Hoog.** 272 releases; actief ontwikkeld (wekelijkse/tweewekelijkse releases); groeiende
   community; funded via commerciële enterprise-editie.
6. **Licentie:** **AGPL-3.0** voor community-editie (bestanden buiten `/enterprise`-directory, OSI-goedgekeurd,
   sterk netwerk-copyleft). Enterprise-features (map `/enterprise`) onder proprietary intuitem Commercial
   Software License. Harde poort: community-editie is echt open source — maar let op copyleft-implicaties
   bij integratie in eigen producten.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar (Docker, on-prem of eigen cloud). Dataresidentie 100%
   in eigen beheer. Ontwikkeld door Frans bedrijf (intuitem). Sterke EU-fit.
8. **Integreerbaarheid:** REST API aanwezig. Exportmogelijkheden voor compliance-rapporten. CLI-tools voor
   import/export van frameworks.
9. **AI-native koppelbaarheid:** Deels. Geen native MCP-server (juni 2026), maar REST API + gestructureerde
   data maken LLM-gebaseerde gap-analyse en rapportage-automatisering goed bouwbaar.
10. **Stack/taal:** Python 59% (Django), Svelte 23% + TypeScript 11% (SvelteKit). PostgreSQL/SQLite.
    Docker/Gunicorn/Caddy deployment.
11. **Fit-score: 3/5 voor RECOVER specifiek** (4/5 als brede GRC-suite). De BCM/ISO 22301-ondersteuning
    is aanwezig maar is een framework-template in een GRC-tool — geen dedicated BCM-platform met lifecycle-
    management, oefening-orchestratie of notificatiestromen. Primair sterk voor GOVERN; voor RECOVER beperkt
    tot compliance-assessments en BIA-registratie.
12. **Bronnen:**
    - https://github.com/intuitem/ciso-assistant-community (AGPL-3.0, 4.1k stars, v3.18.1 geverifieerd)
    - https://www.helpnetsecurity.com/2026/01/14/ciso-assistant-open-source-cybersecurity-management-grc/
    - https://infosecflow.com/blog/open-source-grc-comparison/
    - https://intuitem.gitbook.io/ciso-assistant (BIA-module documentatie)

---

### Long tail — BCM / continuïteit

- **Eramba** (https://eramba.org/) — ⚠️ **BUITEN HARDE POORT: custom proprietary licentie, geen OSI-goedkeuring, GitHub-repo privé.** Heeft BCM-module en wordt breed geciteerd als "open source GRC" maar is source-available, niet open source. Niet aanbevolen.
- **OpenProject** (https://github.com/opf/openproject, GPLv3) — Project- en taakbeheer; geen dedicated BCM-tool, maar inzetbaar voor continuïteitsplan-documentatie en actie-opvolging als generiek wiki/PM-systeem.
- **Nextcloud + documenten** (https://nextcloud.com/) — Geen BCM-tool, maar zelf-hostbare samenwerkingsomgeving bruikbaar voor het beheren van BIA-spreadsheets en continuïteitsplan-documenten; template-gedreven aanpak.

---

## 3. Disaster recovery planning & testing

OSS voor DR-planning (plannen opstellen, beheren, testen, uitvoeren) bestaat nagenoeg niet als dedicated
tool. Wat wél bestaat in OSS zijn: (a) chaos-engineering-tools voor veerkrachttest/failover-validatie,
(b) infrastructuur-replicatie-tools (DRBD, Velero), en (c) template-repositories op GitHub. Geen enkel
OSS-project biedt een volwaardig DR-orchestratie-platform vergelijkbaar met commercieel aanbod (Cutover,
Veeam Recovery Orchestrator, IDR Manager).

### 3.1 LitmusChaos — *primaire aanbeveling: DR-veerkrachttesting voor Kubernetes*

1. **Naam + URL:** LitmusChaos — https://litmuschaos.io/ · https://github.com/litmuschaos/litmus
2. **CSF-functie(s):** RECOVER (DR-testing, veerkrachtvalidatie). Raakt IDENTIFY (risk assessment via
   chaos-experimenten), PROTECT (weerbaarheids-hardening).
3. **Capability:** Cloud-native chaos-engineering-platform voor het induceren van gecontroleerde storingen
   ter validatie van DR-procedures en herstelcapaciteit.
4. **Omschrijving:** CNCF Incubating-project; induceren van chaos-experimenten op pod, netwerk, node,
   storage en applicatieniveau. ChaosHub met pre-built experiments (PodDelete, NetworkChaos, NodeDrain,
   StorageChaos etc.) voor validatie van DR-scenario's. Litmus Probes voor steady-state hypothese-validatie
   (RTO/RPO-verificatie). Prometheus-metrics voor observeerbaarheid van experiment-impact. GitOps-integratie.
   Recentelijk: Litmus MCP Server uitgebracht voor AI-workflow-integratie. Actief: 5.400 GitHub-sterren;
   Q4 2025-update gepubliceerd door CNCF (januari 2026).
5. **Rijpheid:** **Hoog.** CNCF Incubating (promoted 2022); enterprise-adopters: Intuit, Red Hat, NetApp,
   VMware, Flipkart, Ericsson (60+ organisaties).
6. **Licentie:** **Apache-2.0** (OSI-goedgekeurd, permissief). Volledig open source.
7. **EU-soevereiniteit:** ✅ Zelf-hostbaar in eigen K8s-cluster. Geen externe SaaS-afhankelijkheid.
8. **Integreerbaarheid:** Kubernetes CRDs + GraphQL API + Go SDK (litmus-go). Prometheus-metrics. MCP
   Server voor AI-tool-integratie. GitOps (Argo CD, Flux).
9. **AI-native koppelbaarheid:** Ja. Litmus MCP Server gepubliceerd (2025/2026) — directe integratie met
   AI-agents voor het orkestreren van chaos-experimenten via Model Context Protocol.
10. **Stack/taal:** Go (84%), SCSS (12%). Kubernetes-native.
11. **Fit-score: 4/5 voor K8s-omgevingen** (3/5 voor niet-K8s). Uitstekend voor DR-veerkrachttesting in
    container-omgevingen; AI-native koppelbaarheid is een uniek pluspunt. Buiten K8s: beperkt toepasbaar.
12. **Bronnen:**
    - https://github.com/litmuschaos/litmus (Apache-2.0, 5.4k stars geverifieerd)
    - https://litmuschaos.io/ (MCP Server vermelding)
    - https://www.cncf.io/blog/2026/01/22/litmuschaos-q4-2025-update-community-contributions-and-project-progress/
    - https://www.virtualizationhowto.com/2025/07/home-lab-chaos-engineering-unleashed-with-litmuschaos/

---

### 3.2 Chaos Toolkit — *aanbeveling: infrastructure-agnostisch chaos-engineering framework*

1. **Naam + URL:** Chaos Toolkit — https://chaostoolkit.org/ · https://github.com/chaostoolkit/chaostoolkit
2. **CSF-functie(s):** RECOVER (DR-testing, failover-validatie). Raakt IDENTIFY (risico-validatie via
   gecontroleerde chaos).
3. **Capability:** Uitbreidbaar chaos-engineering framework voor het ontwerpen, uitvoeren en analyseren van
   chaos-experimenten op iedere infrastructuur (niet K8s-only).
4. **Omschrijving:** Python-gebaseerd, pluggable framework: experimenten worden declaratief beschreven als
   JSON/YAML-bestanden. Extensies/drivers voor AWS, GCP, Azure, Kubernetes, Cloud Foundry, Service Fabric,
   Slack, Prometheus e.a. Resultaten worden als machine-readable JSON opgeslagen; reporting-plugins
   beschikbaar. Brede OS/infra-ondersteuning maakt het geschikt buiten K8s-context. 2.121 GitHub-sterren.
5. **Rijpheid:** **Middel.** Functioneel volwassen; minder CNCF-institutioneel kader dan LitmusChaos maar
   breder toepasbaar. Actief community-gedreven.
6. **Licentie:** **Apache-2.0** (OSI-goedgekeurd, permissief).
7. **EU-soevereiniteit:** ✅ Volledig lokaal uitvoerbaar; geen externe afhankelijkheden.
8. **Integreerbaarheid:** Python API + CLI. JSON/YAML experiment-definitie. Extensie-ecosystem voor alle
   grote cloud-providers en infra-lagen.
9. **AI-native koppelbaarheid:** Deels. Python API + JSON-output maken LLM-integratie mogelijk; geen
   native MCP-server.
10. **Stack/taal:** Python. Cross-platform.
11. **Fit-score: 3/5.** Goede keuze voor infra-agnostische DR-test-scripting buiten K8s; minder plug-and-
    play dan LitmusChaos; vereist meer eigen experiment-ontwikkeling.
12. **Bronnen:**
    - https://github.com/chaostoolkit/chaostoolkit (Apache-2.0, 2.1k stars geverifieerd)
    - https://steadybit.com/blog/top-chaos-engineering-tools-worth-knowing-about-2025-guide/
    - https://katalon.com/resources-center/blog/chaos-testing-a-complete-guide

---

### Long tail — DR planning & testing

- **Chaos Mesh** (https://github.com/chaos-mesh/chaos-mesh, Apache-2.0, CNCF Incubating) — K8s-native chaos-engineering platform met brede fault-types (pod, netwerk, IO, tijd, stress); goed alternatief voor LitmusChaos bij voorkeur voor een meer K8s-operatornative aanpak.
- **DRBD** (https://linbit.com/drbd/, GPLv2 kernel-module) — Block-level replicatie voor HA + asynchrone off-site DR; geen planningsplatform maar kern-infrastructuur voor DR-failover.
- **disaster-recovery-plan-template** (https://github.com/topics/disaster-recovery) — GitHub-community biedt diverse template-repositories (bv. `disaster-recovery-plan-template`) met BIA-werkbladen en RTO/RPO-tabellen als vertrekpunt; geen tool, wel bruikbaar als documentatie-geraamte.
- **pgBackRest** (https://pgbackrest.org/) — Gespecialiseerd PostgreSQL backup & point-in-time-recovery (PITR) tool; relevant voor database-DR in K8s (zie ook postgres-ha-chaos-lab).

---

## 4. Post-incident review / lessons learned / blameless postmortems

> ⚠️ **Structureel gap: dedicated OSS postmortem-management bestaat nauwelijks.**
> Morgue (Etsy) is de enige historische OSS postmortem-webapp van enige bekendheid — maar is **gearchiveerd
> in 2019** en niet meer onderhouden. Moderne commerciële platformen (Rootly, incident.io, Jeli, PagerDuty)
> domineren dit segment. Open-source incident-management-platforms (OneUptime, IncidentBot) bieden
> postmortem-functionaliteit als onderdeel van een bredere suite, maar zijn niet dedicated postmortem-tools.

### 4.1 OneUptime — *aanbeveling: open-source incident management met postmortem-module*

1. **Naam + URL:** OneUptime — https://oneuptime.com/ · https://github.com/OneUptime/oneuptime
2. **CSF-functie(s):** RESPOND (primair: incident management, on-call). RECOVER via postmortem-templates
   en lessons-learned-documentatie. Multi-functie platform.
3. **Capability:** Volledig open-source observability + incident management platform met ingebouwde
   postmortem-templates en statuspage-communicatie.
4. **Omschrijving:** Breed platform: monitoring, incident management (lifecycle van detectie t/m resolutie),
   on-call scheduling, statuspage, APM, logs/metrics/traces — alles self-hosted. Relevantie voor RECOVER:
   ingebouwde postmortem-templates voor snelle lessons-learned-vastlegging na incidenten; status-communicatie
   naar stakeholders tijdens herstel. Apache-2.0, 7.200 GitHub-sterren; v11.0.3 uitgebracht 17 juni 2026.
   TypeScript-gebaseerd; Helm/Docker Compose deployment.
5. **Rijpheid:** **Hoog.** 7.200 sterren; 38.591 commits; actief dagelijks ontwikkeld; recente releases.
6. **Licentie:** **Apache-2.0** (OSI-goedgekeurd, permissief). Volledig open source.
7. **EU-soevereiniteit:** ✅ Volledig zelf-hostbaar (Helm, Docker Compose). Dataresidentie in eigen beheer.
8. **Integreerbaarheid:** Slack, Jira, GitHub en 5000+ via workflow-automatisering. Prometheus/OpenTelemetry.
   K8s/Docker/Proxmox/Ceph monitoring-agents.
9. **AI-native koppelbaarheid:** Deels. Geen native MCP-server (juni 2026); REST API aanwezig.
10. **Stack/taal:** TypeScript (primair). PostgreSQL. Helm/Docker Compose.
11. **Fit-score: 3/5 voor RECOVER specifiek** (4/5 als gecombineerde RESPOND+RECOVER suite). Postmortem-
    functionaliteit is aanwezig maar niet het primaire focuspunt; sterker als RESPOND-tool. De breedte
    (monitoring + incident + statuspage + postmortem in één) maakt het aantrekkelijk als uniforme suite.
12. **Bronnen:**
    - https://github.com/OneUptime/oneuptime (Apache-2.0, 7.2k stars, v11.0.3 geverifieerd)
    - https://oneuptime.com/
    - https://openapps.pro/apps/oneuptime

---

### 4.2 IncidentBot — *aanbeveling: ChatOps-gedreven incident + postmortem (Slack/Matrix)*

1. **Naam + URL:** IncidentBot — https://github.com/incidentbot/incidentbot
2. **CSF-functie(s):** RESPOND (incident management via ChatOps). RECOVER via automatisch opbouwen van
   postmortem-documentbasis.
3. **Capability:** Open-source incident management framework rondom een ChatOps-bot (Slack/Matrix) met
   automatische postmortem-document-generatie.
4. **Omschrijving:** Python-gebaseerde bot die incident-kanalen aanmaakt, rollen toewijst, severity
   beheert en na afloop automatisch een postmortem-documentbasis opbouwt. Integraties: Confluence, Jira,
   GitLab, Statuspage, PagerDuty, Zoom, Phare. CalVer-versioning; container-registry naar GHCR
   gemigreerd (juni 2026). MIT-licentie; 164 sterren; laatste release 2026.06.01.
5. **Rijpheid:** **Laag-middel.** Functioneel maar beperkte community (164 sterren). Actief onderhouden
   (juni 2026). Geschikt voor teams die al zwaar op Slack/Matrix draaien.
6. **Licentie:** **MIT** (OSI-goedgekeurd, permissief). Volledig open source.
7. **EU-soevereiniteit:** ⚠️ Zelf-hostbaar (Python-app), maar postmortem-documenten worden naar Confluence
   geschreven (kan Confluence Server/Data Center on-prem zijn). Slack-afhankelijkheid introduceert mogelijk
   non-EU-dataverwerking — zelf beoordelen per deploymentmodel.
8. **Integreerbaarheid:** Slack/Matrix webhooks. Confluence, Jira, GitLab, PagerDuty, Statuspage, Zoom API.
9. **AI-native koppelbaarheid:** Nee (geen native MCP/AI).
10. **Stack/taal:** Python (96%). Docker-deployable.
11. **Fit-score: 2/5.** Beperkte community en ster-count; de ChatOps-postmortem-aanpak is waardevol maar
    de tool is jong en licht. Alleen geschikt als de organisatie al op Slack/Matrix + Confluence zit.
12. **Bronnen:**
    - https://github.com/incidentbot/incidentbot (MIT, 164 stars, release 2026.06.01 geverifieerd)

---

### Long tail — Postmortems / lessons learned

- **Morgue** (https://github.com/etsy/morgue, MIT) — ⚠️ **Gearchiveerd (2019), niet meer onderhouden.** Historisch de standaard OSS postmortem-webapp (PHP, 1.000 sterren); timeline, remediation, JIRA-integratie. Niet meer bruikbaar voor productie zonder eigen fork/onderhoud.
- **postmortem-templates** (https://github.com/dastergon/postmortem-templates, 1.4k sterren) — Curated collectie postmortem-templates (markdown); geen applicatie, maar het meest geciteerde OSS-postmortem-vertrekpunt.
- **danluu/post-mortems** (https://github.com/danluu/post-mortems, 7k+ sterren) — Curated database van publieke postmortems van bekende technologiebedrijven; niet een tool maar een kennisbron.
- **Parabol** (https://github.com/ParabolInc/parabol, AGPLv3) — Open-source retrospective/meeting-tool voor Agile teams; kan voor lessons-learned-meetings ingezet worden maar is geen dedicated postmortem-platform.
- **Google SRE Postmortem Culture** (https://sre.google/sre-book/postmortem-culture/) — Niet een tool maar het normatieve raamwerk (Google SRE-boek) waarop de meeste templates zijn gebaseerd; essentieel referentiemateriaal.

---

## 5. Multi-functie tools (cross-categorie — deduplicatie)

De volgende tools raken meerdere CSF-functies en zijn relevant voor RECOVER maar primair elders
gecatalogiseerd:

| Tool | Primaire CSF-plek | RECOVER-raakvlak |
|------|------------------|-----------------|
| **CISO Assistant** | GOVERN | ISO 22301-framework, BIA-module |
| **OneUptime** | RESPOND | Postmortem-templates, statuspage tijdens herstel |
| **DRBD** | PROTECT | HA-replicatie als DR-basis |
| **Velero** | RECOVER/PROTECT | K8s backup én cluster-migratie |
| **OpenProject** | GOVERN | Continuïteitsplan-documentatie als generiek PM-systeem |

---

## 6. Niet-gedekt / gaps

Dit is de meest informatieve paragraaf voor de blueprint: de schaarste is structureel en voorspelbaar.

### 6.1 Dedicated BCM/ISO 22301-managementsoftware (ernstige gap)

**Wat ontbreekt:** Een volledig open-source BCM-platform dat de ISO 22301-levenscyclus ondersteunt:
BIA-workflows (impact- en urgentiebeoordeling per bedrijfsproces), continuïteitsplan-lifecycle-management
(versioning, goedkeuringsflows, distributie), BCM-oefeningen plannen en logging, herstelobjectivenbeheer
(RTO/RPO-registratie per proces), en compliance-rapportage naar ISO 22301.

**Wat bestaat:** Enkel CISO Assistant (als GRC-compliance-tool met ISO 22301-framework-template). Dit is
*geen* dedicated BCM-platform; het is een compliance-check-instrument. De volledige BCM-lifecycle wordt
*niet* gedekt.

**Commerciële alternatieven** die dit wel dekken: Fusion Risk Management, Riskonnect, Castellan, ServiceNow
BCM, Everbridge, BCMMetrics, autoResilience. Geen van deze is open source.

**Eramba-disclaimer:** Eramba heeft een BCM-module en wordt in vrijwel alle vergelijkende artikelen als
"open source GRC" geciteerd. Na verificatie is de community-editie **niet OSI-compliant** (custom
licentie, geen herdistributie, private broncode). De tool is uitsluitend als "bron-beschikbaar" te
kwalificeren en valt buiten de harde poort van dit onderzoek.

### 6.2 DR-planningsplatform / runbook-orchestratie (ernstige gap)

**Wat ontbreekt:** Een open-source DR-planningplatform dat DR-plannen opslaat, beheert en test-runs
registreert; runbook-automatisering met stap-voor-stap-uitvoering tijdens een DR-event; failover-
orchestratie met progressiebeheer; RTO/RPO-tracking per systeem; auditlog van DR-tests.

**Wat bestaat:** Alleen chaos-engineering-tools (LitmusChaos, Chaos Toolkit, Chaos Mesh) voor het
valideren of systemen veerkrachtig zijn. Dit is slechts een deelaspect van DR-testing; de bredere
DR-plannings- en -uitvoeringslaag ontbreekt volledig in OSS.

**Commerciële alternatieven:** Cutover (DR runbook automation), Veeam Recovery Orchestrator, IDR Manager
(SVA), Druva Automated DR. Geen open source.

### 6.3 Dedicated postmortem-managementplatform (matige gap)

**Wat ontbreekt:** Een zelf-hostbare, dedicated post-incident review webapp met: gestructureerde postmortem-
templates, tijdlijn-reconstructie, contributing factor-analyse (5-why/fishbone), actie-opvolging,
kennisbase van eerdere postmortems, zoekfunctionaliteit.

**Wat bestaat:** Templates (markdown), een gearchiveerde PHP-app (Morgue), en postmortem-modules in
bredere incident-management-suites (OneUptime, IncidentBot). Er is geen volwaardige dedicated OSS-
postmortem-webapp in actieve ontwikkeling.

**Commerciële alternatieven:** Jeli (nu PagerDuty), Rootly (postmortem-module), incident.io (postmortem-
module), Atlassian Statuspage + Confluence-integraties. Geen volledig open source.

**Partiële mitigatie:** Gecombineerde inzet van OneUptime (incident + postmortem-template) + een wiki
(Wiki.js, BookStack, Outline — alle OSS) voor kennisbase-opbouw biedt een bruikbaar, zij het niet
geïntegreerd, alternatief.

### 6.4 BIA-tool (ernstige gap)

**Wat ontbreekt:** Gespecialiseerde open-source software voor Business Impact Analysis: processenregistratie,
impact-/urgentiescores (financieel, operationeel, reputationeel), afhankelijkheidsanalyse (systemen,
leveranciers), herstelprioriteiten, RTO/RPO-doelstellingen, managementrapportage.

**Wat bestaat:** Spreadsheet-templates (TechTarget, Smartsheet), CISO Assistant als compliance-check voor
ISO 22301. Geen dedicated BIA-tool in OSS-ecosysteem.

### 6.5 Samenvatting gap-matrix

| Capability | OSS-beschikbaarheid | Ernst gap | Beste huidige OSS-alternatief |
|------------|--------------------|-----------|-----------------------------|
| File/object backup | ✅ Ruim (restic, BorgBackup, Duplicati) | — | restic |
| K8s backup/DR | ✅ Ruim (Velero) | — | Velero |
| Block-replicatie (HA/DR) | ✅ (DRBD) | — | DRBD |
| Chaos/veerkrachttesting | ✅ Goed (LitmusChaos, Chaos Toolkit, Chaos Mesh) | — | LitmusChaos (K8s) |
| Postmortem-module (in suite) | ⚠️ Beperkt (OneUptime, IncidentBot) | Matig | OneUptime |
| Dedicated postmortem-webapp | ❌ Nauwelijks (Morgue: archived) | Matig | — |
| ISO 22301-compliance-check | ⚠️ Beperkt (CISO Assistant) | Matig | CISO Assistant |
| BCM lifecycle-management | ❌ Afwezig | Ernstig | — |
| BIA-tool | ❌ Afwezig | Ernstig | — |
| DR-planningplatform | ❌ Afwezig | Ernstig | — |
| DR runbook-orchestratie | ❌ Afwezig | Ernstig | — |

---

*Onderzoek uitgevoerd juni 2026. Bronnen geverifieerd via directe GitHub-raadpleging en geciteerde
artikelen. Licenties geverifieerd via repo-LICENSE-bestanden of officiële projectpagina's.*
