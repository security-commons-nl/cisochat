# PROTECT — Open-Source Tooling Survey

**CSF-functie:** PROTECT (PR)  
**Scope:** Open-source tooling voor de PROTECT-functie van NIST CSF 2.0. Dekt vijf sub-categorieën: (1) maatregelen-/control-management, (2) security awareness & phishing-simulatie, (3) IAM / access-governance, (4) configuratie-baselines & hardening, (5) policy-as-code-enforcement. Peildatum juni 2026.  
**Ordeningsframe:** NIST CSF 2.0  
**Licentie-filter:** OSI-goedgekeurd open source. Open-core: alleen community-editie beoordeeld; betaalmuur genoteerd. Source-available (BSL/SSPL/Commons Clause/CC-NC/Elastic) = afgewezen of apart geflagd.

> **Dedup-notitie:** CISO Assistant (zie ook GOVERN-onderzoek) dekt meerdere CSF-functies (GOVERN + PROTECT PR.AA). OpenSCAP + ComplianceAsCode werken als complementair ecosysteem en worden hier samen behandeld. Lynis overlapt deels met IDENTIFY (ID.RA).

---

## 1. Maatregelen-/control-management

*Welke open-source GRC-tools ondersteunen het beheer van PROTECT-controls (beleidsmaatregelen, control-frameworks, interne audits)?*

### Top tools

#### CISO Assistant (community)

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | CISO Assistant — https://github.com/intuitem/ciso-assistant-community |
| **2. CSF-functie(s)** | GOVERN (GV), PROTECT (PR), IDENTIFY (ID) |
| **3. Capability** | Control-management / GRC |
| **4. Omschrijving** | One-stop GRC-platform voor risicobeheer, compliance, audit, AppSec, TPRM, BIA en privacy. Ondersteunt 100+ frameworks inclusief NIST CSF v1.1 en v2.0, NIST SP 800-53 rev5, ISO 27001, GDPR, NIS2. Community-editie bevat alle kernfunctionaliteit zonder intentionele feature-locks. |
| **5. Rijpheid** | Actief ontwikkeld; release v3.18.1 uitgebracht 15 juni 2026; 4.100+ GitHub stars; 747 forks. Gestart 2023. |
| **6. Licentie** | AGPL-3.0 (community); intuitem Commercial Software License (bestanden in `/enterprise`-map). Open-core: enterprise-map bevat extra features (AI-agenten, geavanceerde rapportage), maar community-editie is volledig functioneel. |
| **7. EU-soevereiniteit** | Volledig self-hosted (Docker). Geen SaaS-vereiste. Gegevens blijven op eigen infra. ✅ |
| **8. Integreerbaarheid** | REST API, Python/Svelte-stack, exportfunctionaliteit voor audits en rapporten. |
| **9. AI-native koppelbaarheid** | Deels — enterprise-editie heeft ingebouwde AI-agenten; community kan via eigen LLM-integratie worden uitgebreid door de API. |
| **10. Stack/taal** | Python (59%), Svelte (24%), TypeScript (11%) |
| **11. Fit-score** | **5/5** — Meest complete open-source GRC-tool voor NIST CSF 2.0, actief onderhouden, volledig self-hosted, EU-soeverein, brede frameworkdekking. |
| **12. Bronnen** | https://github.com/intuitem/ciso-assistant-community · https://infosecflow.com/blog/open-source-grc-comparison/ |

---

#### Eramba (community edition)

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | Eramba — https://github.com/eramba · https://www.eramba.org |
| **2. CSF-functie(s)** | GOVERN (GV), PROTECT (PR), IDENTIFY (ID) |
| **3. Capability** | Control-management / GRC |
| **4. Omschrijving** | Enterprise GRC-platform (gestart 2007 door CISOs); community-editie gratis zonder gebruikers- of datalimieten. Dekt risicobeheer, compliancebeheer, interne audits, dataPrivacy, bewustzijnstraining en incidentbeheer. |
| **5. Rijpheid** | Zeer volwassen (opgericht 2007); actieve community. Geen eigen GitHub-repo gevonden voor community-editie — distributiepunt is www.eramba.org; forks aanwezig op GitHub (bijv. sys02/eramba). ⚠️ Verificatie: LICENSE.txt bevestigt GPL-2.0. |
| **6. Licentie** | GPL-2.0 (community-editie). Enterprise-editie: €2.500–5.000/jaar. Open-core: geavanceerde RBAC, 5+ automatiseringsworkflows, configureerbare rapporten en AI-agenten zitten achter betaalmuur. |
| **7. EU-soevereiniteit** | Volledig self-hosted (Docker). ✅ |
| **8. Integreerbaarheid** | Beperkt in community; API-toegang in enterprise-editie. ⚠️ |
| **9. AI-native koppelbaarheid** | Nee in community; AI-agenten alleen enterprise. |
| **10. Stack/taal** | PHP (CakePHP-framework) |
| **11. Fit-score** | **3/5** — Volwassen en bewezen platform, maar API en geavanceerde integratie zitten achter betaalmuur; NIST CSF-mapping minder expliciet dan CISO Assistant; lage GitHub-transparantie. |
| **12. Bronnen** | https://github.com/sys02/eramba/blob/master/LICENSE.txt · https://infosecflow.com/blog/open-source-grc-comparison/ · https://grc-review.com/products/eramba |

---

### Long tail — maatregelen-/control-management

| Tool | URL | Noot |
|------|-----|------|
| **SimpleRisk Core** | https://github.com/simplerisk/code | MPL-2.0; 101 stars; PHP; open-core (API en rapportage achter betaalmuur via "Extras"). Beperkt voor grote PROTECT-dekking. |
| **OpenControl / Compliance Masonry** | https://github.com/opencontrol/compliance-masonry | YAML-gebaseerde control-documentatie in code; geschikt als "compliance-as-code" aanvulling op GRC-tools; geen UI. Apache-2.0. |

---

## 2. Security awareness & phishing-simulatie

*Tools voor het simuleren van phishing-aanvallen en het leveren van security awareness-training.*

### Top tools

#### Gophish

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | Gophish — https://github.com/gophish/gophish · https://getgophish.com |
| **2. CSF-functie(s)** | PROTECT (PR.AT) |
| **3. Capability** | Phishing-simulatie |
| **4. Omschrijving** | De facto standaard open-source phishing-toolkit; ontworpen voor pentesters en security-teams. Biedt volledige campagnebeheer via web-UI: e-mailtemplates, landingspagina's, click/credential-tracking en rapportage. Cross-platform (Windows/Mac/Linux), Docker-support. |
| **5. Rijpheid** | ⚠️ **Onderhoudszorg:** Laatste release v0.12.1 uitgebracht op 14 september 2022 — meer dan 3,5 jaar geleden. Geen actieve releases sindsdien ondanks 13.900+ stars. Technisch functioneel maar niet actief doorontwikkeld. |
| **6. Licentie** | MIT ✅ — volledig permissief, OSI-goedgekeurd. |
| **7. EU-soevereiniteit** | Volledig self-hosted. Geen externe afhankelijkheden. ✅ |
| **8. Integreerbaarheid** | REST API voor campagnebeheer; CLI-deployment; Docker. Kan gekoppeld worden aan SMTP-relays naar keuze. |
| **9. AI-native koppelbaarheid** | Nee — geen ingebouwde AI; templates kunnen extern worden gegenereerd en ingevoerd. |
| **10. Stack/taal** | Go (62%), JavaScript (26%), HTML (12%) |
| **11. Fit-score** | **3/5** — Beste volledig open-source phishing-tool qua functies en permissieve licentie, maar de stagnerende release-cadans (laatste release 2022) is een serieus bezwaar voor productiegebruik. Vereis eigen hardening en monitoring. |
| **12. Bronnen** | https://github.com/gophish/gophish · https://autophish.io/blog/open-source-phishing-simulation-tools-vs-managed-solutions |

---

#### Moodle (als awareness-LMS)

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | Moodle — https://moodle.org · https://github.com/moodle/moodle |
| **2. CSF-functie(s)** | PROTECT (PR.AT) |
| **3. Capability** | Security awareness-training / LMS |
| **4. Omschrijving** | Wereldwijd meest gebruikte open-source LMS (300+ miljoen gebruikers). Ondersteunt SCORM 1.2 natively (betrouwbaar), SCORM 2004 beperkt. Security awareness-modules (SCORM-pakketten van externe aanbieders of zelfgebouwd) kunnen worden uitgerold. Volledig self-hosted. |
| **5. Rijpheid** | Zeer volwassen; actief onderhouden; grote community; PHP-gebaseerd. |
| **6. Licentie** | GPL-3.0 ✅ — copyleft maar volledig open source. |
| **7. EU-soevereiniteit** | Volledig self-hosted. Geen SaaS-vereiste. ✅ |
| **8. Integreerbaarheid** | REST API, LTI, LDAP/SAML/OIDC SSO, Webhooks. Kan gekoppeld worden aan Gophish via eigen integratie (redirect-URL na phishing-klik naar Moodle-cursus). |
| **9. AI-native koppelbaarheid** | Deels — Moodle AI subsystems (plugins) beschikbaar; geen native GenAI-integratie out-of-the-box. |
| **10. Stack/taal** | PHP (primair), JavaScript |
| **11. Fit-score** | **4/5** — Robuuste, bewezen LMS voor awareness-content; gecombineerd met Gophish en SCORM-content een volwaardig open-source awareness-programma. Nadeel: geen geïntegreerde phishing-simulatie; vereist combinatie met Gophish of vergelijkbaar. |
| **12. Bronnen** | https://moodle.org · https://ransomleak.com/blog/open-source-lms-security-training/ |

---

### Long tail — security awareness & phishing-simulatie

| Tool | URL | Noot |
|------|-----|------|
| **Social Engineer Toolkit (SET)** | https://github.com/trustedsec/social-engineer-toolkit | BSD-3-Clause; phishing + social engineering voor pentest; geen analytics of trainingsworkflow; niet geschikt voor breed awareness-programma. |
| **Phishing Frenzy** | https://github.com/pentestgeek/phishing-frenzy | GPL; ⚠️ project **niet meer actief onderhouden** — veiligheidsbezwaren; niet aanbevolen. |
| **King Phisher** | https://github.com/rsmusllp/king-phisher | BSD-3-Clause; geavanceerder dan Gophish maar ook inactief (laatste commit 2022). |
| **Chamilo / ILIAS** | https://chamilo.org · https://www.ilias.de | GPL; alternatieve open-source LMS-platforms; ILIAS sterker in SCORM 2004; beide self-hostable EU-soeverein. |

---

## 3. IAM / access-governance

*Identity & Access Management, SSO, MFA, directory-services, access-governance.*

### Top tools

#### Keycloak

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | Keycloak — https://github.com/keycloak/keycloak · https://www.keycloak.org |
| **2. CSF-functie(s)** | PROTECT (PR.AA, PR.AC) |
| **3. Capability** | IAM / access-governance |
| **4. Omschrijving** | De meest volwassen en uitgebreide open-source IAM-oplossing. Ondersteunt OIDC, SAML 2.0, OAuth 2.0, LDAP-federatie, Kerberos, MFA, fine-grained authorization. Ontwikkeld door Red Hat (nu IBM), CNCF-ecosysteem. Extensible via SPI (Service Provider Interface). |
| **5. Rijpheid** | Zeer volwassen; gestart 2013; 35.000+ GitHub stars; release 26.6.3 uitgebracht 4 juni 2026; 31.000+ commits; 1.000+ contributors. |
| **6. Licentie** | Apache-2.0 ✅ — volledig permissief, OSI-goedgekeurd. Geen open-core; geen features achter betaalmuur. Red Hat biedt commerciële support maar de software zelf is volledig open. |
| **7. EU-soevereiniteit** | Volledig self-hosted. Geen cloud-afhankelijkheid. ✅ Veelgebruikt in EU-overheidsomgevingen. |
| **8. Integreerbaarheid** | Uitgebreide REST API; Admin CLI; Kubernetes Operator; Helm chart; integratie met Ansible, Terraform, HashiCorp Vault; native LDAP/AD-federatie. |
| **9. AI-native koppelbaarheid** | Deels — Keycloak kan als identity provider dienen voor AI-platforms (OIDC/OAuth2). Geen ingebouwde AI-features; via token-gebaseerde autorisatie koppelbaar aan AI-workloads. |
| **10. Stack/taal** | Java (92%, Quarkus-runtime) |
| **11. Fit-score** | **5/5** — Rijpste open-source IAM-oplossing; Apache-2.0; geen betaalmuur; volledig EU-soeverein; uitstekende integratie; breed gedragen in enterprise en overheid. |
| **12. Bronnen** | https://github.com/keycloak/keycloak · https://www.positioniseverything.net/6-best-open-source-iam-tools-in-2026/ |

---

#### Authentik

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | authentik — https://github.com/goauthentik/authentik · https://goauthentik.io |
| **2. CSF-functie(s)** | PROTECT (PR.AA, PR.AC) |
| **3. Capability** | IAM / access-governance |
| **4. Omschrijving** | Moderne, self-hosted Identity Provider gericht op gebruiksgemak en flexibele authentication flows. Ondersteunt SAML, OAuth2/OIDC, LDAP, RADIUS. Populair als alternatief voor Okta/Auth0 in self-hosted omgevingen. "Authentication glue" voor diverse applicaties. |
| **5. Rijpheid** | Actief; gestart 2019; 22.000+ GitHub stars; release 2026.5.3 uitgebracht 10 juni 2026; 300+ contributors. |
| **6. Licentie** | MIT (core community-editie) ✅; enterprise-features onder proprietary EE License (bestanden in `/enterprise`). ⚠️ Open-core: enterprise-editie positioneert zich als vervanging van Okta/Auth0/Entra ID met extra compliance- en supportfeatures. De community MIT-kern is volledig functioneel als IdP. |
| **7. EU-soevereiniteit** | Volledig self-hosted (Docker Compose, Kubernetes/Helm). ✅ |
| **8. Integreerbaarheid** | REST API; Python (54%), TypeScript (35%), Go; LDAP-proxy, SCIM-provisioning in development. |
| **9. AI-native koppelbaarheid** | Nee — geen native AI-features; koppelbaar als OIDC IdP voor AI-platforms. |
| **10. Stack/taal** | Python (54%), TypeScript (35%), Go (4%), Rust (2%) |
| **11. Fit-score** | **4/5** — Moderne UX, actief ontwikkeld, MIT-kern vrij permissief, volledig self-hosted. Lichte aftrek voor open-core (enterprise-map) en lagere rijpheid dan Keycloak. |
| **12. Bronnen** | https://github.com/goauthentik/authentik · https://wz-it.com/en/blog/authentik-vs-zitadel-identity-provider-comparison/ |

---

### Long tail — IAM / access-governance

| Tool | URL | Noot |
|------|-----|------|
| **Zitadel** | https://github.com/zitadel/zitadel | ⚠️ **Licentiewaarschuwing:** Apache-2.0 → AGPL-3.0 gewijzigd per v3.0 (maart 2025). Copyleft; modificaties moeten openbaar. 14.100 stars; actief; cloud-native multi-tenant IAM. Voor organisaties zonder SaaS-integratie acceptabel. |
| **FreeIPA** | https://www.freeipa.org | GPL-3.0; Linux-centrisch (Kerberos, LDAP, DNS, SSSD); uitstekend voor on-prem Linux-infrastructuur. Minder geschikt als generieke OIDC IdP. |
| **Gluu** | https://gluu.org | Apache-2.0 (core); open-core; complexere deploymentvereisten; 1.500 stars; mindere community dan Keycloak. |
| **Casdoor** | https://github.com/casdoor/casdoor | Apache-2.0; lichtgewicht IAM met UI; 10.000 stars; groeiende community. |

---

## 4. Configuratie-baselines & hardening

*Tools voor het scannen, beoordelen en hardenen van systemen tegen beveiligingsbaselines (CIS, STIG, NIST).*

### Top tools

#### OpenSCAP + ComplianceAsCode/content

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | OpenSCAP — https://github.com/OpenSCAP/openscap · https://www.open-scap.org  ComplianceAsCode — https://github.com/ComplianceAsCode/content |
| **2. CSF-functie(s)** | PROTECT (PR.IP) |
| **3. Capability** | Configuratie-baselines & hardening |
| **4. Omschrijving** | **OpenSCAP** is een NIST-gecertificeerde SCAP 1.2-toolkit (LGPL-2.1) voor het scannen, valideren en rapporteren van compliance tegen XCCDF/OVAL-profielen. **ComplianceAsCode/content** levert de SCAP-inhoud: kant-en-klare security-profielen voor CIS, DISA STIG, PCI-DSS en NIST SP 800-53 voor RHEL, Ubuntu, Debian, SUSE, Kubernetes/OpenShift. Genereert ook Ansible playbooks en Bash remediatiescripts uit dezelfde bronbestanden. Samen vormen ze het meest complete open-source compliance-automatisering ecosysteem. |
| **5. Rijpheid** | Zeer volwassen. OpenSCAP: release 1.4.4 (april 2026); 1.700+ stars; LGPL-2.1; NIST-gecertificeerd. ComplianceAsCode: release v0.1.81 (1 juni 2026); 2.700+ stars; actief. |
| **6. Licentie** | OpenSCAP: LGPL-2.1 ✅. ComplianceAsCode: ⚠️ Nader te verifiëren — repo vermeld LICENSE-file maar SPDX-identifier niet expliciet geëxtraheerd; inhoud bevat meerdere componenten. Check: https://github.com/ComplianceAsCode/content/blob/master/LICENSE. |
| **7. EU-soevereiniteit** | Volledig lokaal/on-prem uitvoerbaar. Geen externe services. ✅ |
| **8. Integreerbaarheid** | CLI (`oscap scan`, `oscap-report`); Ansible-integratie via gegenereerde playbooks; Red Hat Satellite/Ansible Automation Platform-integratie; output in HTML, XML, ARF. |
| **9. AI-native koppelbaarheid** | Nee direct; scan-output (XML/JSON) kan als compliance-input voor AI-dashboards dienen. |
| **10. Stack/taal** | OpenSCAP: XSLT (72%), C (20%). ComplianceAsCode: Python, YAML, Jinja2. |
| **11. Fit-score** | **5/5** — Gouden standaard voor open-source compliance-scanning; NIST-gecertificeerd; volledig EU-soeverein; actief onderhouden; rijkste profile-bibliotheek beschikbaar. Linux-only (⚠️ Windows-support vervallen per feb 2022). |
| **12. Bronnen** | https://github.com/OpenSCAP/openscap · https://github.com/ComplianceAsCode/content · https://www.open-scap.org/security-policies/choosing-policy/ · https://oneuptime.com/blog/post/2026-03-04-automate-rhel-security-hardening-ansible-openscap/ |

---

#### Lynis

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | Lynis — https://github.com/CISOfy/lynis · https://cisofy.com/lynis |
| **2. CSF-functie(s)** | PROTECT (PR.IP), IDENTIFY (ID.RA) |
| **3. Capability** | Configuratie-baselines & hardening (security audit) |
| **4. Omschrijving** | Agentloze security audittool voor Linux, macOS, BSD en andere Unix-systemen. Voert 171 checks uit op community-editie (211 in enterprise), geeft hardening-aanbevelingen en ondersteunt compliance-testing voor ISO 27001, PCI-DSS, HIPAA. Geen compilation nodig; pure shell-script. Breed inzetbaar als eerste beveiligingsscan van systemen. |
| **5. Rijpheid** | Zeer volwassen; gestart 2007; 15.800+ GitHub stars; release 3.1.6 (oktober 2025). ⚠️ Opmerking: versie 3.1.6 is de meest recente — cadans vertraagd in 2026; check actieve ontwikkeling. |
| **6. Licentie** | GPL-3.0 ✅ (community). Open-core: Enterprise-editie (€90+/jaar) voegt 40 extra tests, hardening snippets, centraal dashboarding, uitgebreide plugins (Docker, PAM, systemd, firewall) en professionele support toe. Community-editie functioneel voor single-systeem scanning. |
| **7. EU-soevereiniteit** | Volledig lokaal uitvoerbaar. ✅ |
| **8. Integreerbaarheid** | CLI; output in JSON/plaintext; integreerbaar met Ansible, SIEM-systemen, CI/CD pipelines. |
| **9. AI-native koppelbaarheid** | Nee — auditoutput kan als input dienen voor AI-analyse. |
| **10. Stack/taal** | Shell (100%) |
| **11. Fit-score** | **4/5** — Bewezen tool voor single-systeem auditing; eenvoudig in gebruik; breed draaibaar; GPL-3.0 copyleft. Aftrek voor open-core (geavanceerde plugins en 40 extra checks achter betaalmuur) en vertraagde 2026-cadans. |
| **12. Bronnen** | https://github.com/CISOfy/lynis · https://cisofy.com/compare/lynis-and-lynis-enterprise/ · https://en.wikipedia.org/wiki/Lynis |

---

#### Ansible Collection devsec.hardening

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | devsec.hardening — https://github.com/dev-sec/ansible-collection-hardening |
| **2. CSF-functie(s)** | PROTECT (PR.IP) |
| **3. Capability** | Configuratie-hardening (Infrastructure-as-Code) |
| **4. Omschrijving** | "Battle-tested" Ansible-collectie met rollen voor OS hardening, SSH hardening, nginx hardening, MySQL hardening. Automatiseert systeemconfiguratie conform DevSec Baselines (gebaseerd op CIS, BSI, NIST-aanbevelingen). Output kan gevalideerd worden via InSpec/OpenSCAP. Onderdeel van het bredere dev-sec.io framework dat ook Chef Inspec baselines levert. |
| **5. Rijpheid** | Actief; release 10.6.0 uitgebracht 26 mei 2026; 5.400+ GitHub stars. |
| **6. Licentie** | Apache-2.0 ✅ — volledig permissief. Geen open-core. |
| **7. EU-soevereiniteit** | Volledig lokaal uitvoerbaar. Ansible-rollen runnen on-prem. ✅ |
| **8. Integreerbaarheid** | Native Ansible Galaxy-integratie; CLI (`ansible-playbook`); koppelbaar aan AWX/AAP, CI/CD pipelines, Terraform. Combineert goed met OpenSCAP voor scan → harden → rescan-cyclus. |
| **9. AI-native koppelbaarheid** | Nee direct; Ansible playbooks kunnen door AI-tools gegenereerd/aangevuld worden (bijv. via Ansible Lightspeed). |
| **10. Stack/taal** | YAML (Ansible), Python |
| **11. Fit-score** | **4/5** — Uitstekend voor geautomatiseerde hardening in IaC-workflows; Apache-2.0; actief; EU-soeverein. Aftrek: vereist Ansible-kennis; geen UI; geen standalone compliance-scanning (complementair aan OpenSCAP). |
| **12. Bronnen** | https://github.com/dev-sec/ansible-collection-hardening · https://evanlovescloud.com/a-guide-on-automating-cis-compliance-for-ubuntu-with-ansible-lockdown |

---

### Long tail — configuratie-baselines & hardening

| Tool | URL | Noot |
|------|-----|------|
| **Wazuh (configuratie-assessment)** | https://github.com/wazuh/wazuh | GPL-2.0; ook IDENTIFY/DETECT; bevat SCA (Security Configuration Assessment) module als onderdeel van bredere SIEM-stack. ⚠️ Open-core: centrale Wazuh-dashboard/cloud achter betaalmuur. |
| **InSpec / Chef Compliance** | https://github.com/inspec/inspec | Apache-2.0; Progress Chef; compliance-as-code tests; dev-sec baselines beschikbaar; goede CI/CD-integratie. |
| **CIS-CAT Lite** | https://www.cisecurity.org/cybersecurity-tools/cis-cat-pro | ⚠️ **Geen open source** — CIS-CAT Lite is een gratis maar proprietary tool van CIS; vermeld als toelichting maar valt buiten OSS-filter. CIS Pro = betaald. Gebruik OpenSCAP + ComplianceAsCode als open-source alternatief. |

---

## 5. Policy-as-code-enforcement

*Technische afdwinging van beveiligingsbeleid in code, met name gericht op cloud-native/Kubernetes-omgevingen. Diepte zit in GOVERN-onderzoek; hier kort gedekt.*

### Top tools

#### Open Policy Agent (OPA)

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | OPA — https://github.com/open-policy-agent/opa · https://www.openpolicyagent.org |
| **2. CSF-functie(s)** | PROTECT (PR.AC, PR.IP), GOVERN (GV.PO) |
| **3. Capability** | Policy-as-code-enforcement |
| **4. Omschrijving** | Generieke, open-source policy engine die beleid als code uitdrukt in Rego (declaratieve taal). Toepasbaar op Kubernetes admission control (via OPA Gatekeeper), API gateways, Terraform-validatie, Envoy/Istio, CI/CD pipelines en meer. CNCF Graduated project. |
| **5. Rijpheid** | Zeer volwassen; CNCF Graduated (hoogste rijpheidsniveau); breed geadopteerd in cloud-native omgevingen. |
| **6. Licentie** | Apache-2.0 ✅ — volledig permissief. OPA Gatekeeper (https://github.com/open-policy-agent/gatekeeper): Apache-2.0; 4.200+ stars. |
| **7. EU-soevereiniteit** | Volledig self-hosted; geen cloud-afhankelijkheid. ✅ |
| **8. Integreerbaarheid** | HTTP-API (port 8181), Go-library, CLI (`opa eval`), Docker. Gatekeeper werkt als Kubernetes Admission Controller via CRDs. |
| **9. AI-native koppelbaarheid** | Deels — OPA-policies kunnen AI/ML-workloads en -API's bewaken; geen native GenAI; via Rego-regels koppelbaar aan elke policy-beslissing. |
| **10. Stack/taal** | Go |
| **11. Fit-score** | **5/5** — De open standaard voor policy-as-code; Apache-2.0; CNCF Graduated; breed inzetbaar buiten Kubernetes; uitstekende integratie. |
| **12. Bronnen** | https://www.openpolicyagent.org/docs · https://github.com/open-policy-agent/opa · https://github.com/open-policy-agent/gatekeeper |

---

#### Kyverno

| Veld | Waarde |
|------|--------|
| **1. Naam + URL** | Kyverno — https://github.com/kyverno/kyverno · https://kyverno.io |
| **2. CSF-functie(s)** | PROTECT (PR.AC, PR.IP) |
| **3. Capability** | Policy-as-code-enforcement (Kubernetes-native) |
| **4. Omschrijving** | Kubernetes-native policy engine: policies worden als YAML geschreven (geen Rego), direct als Kubernetes-objecten. Valideert, muteert, genereert en ruimt Kubernetes-resources op. Verifieert ook container image-signaturen (supply chain security). CNCF Incubating project. |
| **5. Rijpheid** | Actief; CNCF Incubating; release v1.18.1 (18 mei 2026); 7.800+ stars. Kyverno 1.17 (feb 2026) promoveert CEL policy engine van beta naar v1. |
| **6. Licentie** | Apache-2.0 ✅ — volledig permissief. Geen open-core. |
| **7. EU-soevereiniteit** | Volledig self-hosted in Kubernetes-cluster. ✅ |
| **8. Integreerbaarheid** | Native Kubernetes API; kubectl-plugin; kustomize-integratie; background scanning; CI/CD via Kyverno CLI. |
| **9. AI-native koppelbaarheid** | Nee direct; policies kunnen AI-deployments op K8s bewaken (resource-limieten, image-signaturen). |
| **10. Stack/taal** | Go |
| **11. Fit-score** | **4/5** — Laagste drempel voor K8s policy-as-code (YAML vs Rego); actief; Apache-2.0. Aftrek: Kubernetes-only scope; minder generiek dan OPA. |
| **12. Bronnen** | https://github.com/kyverno/kyverno · https://araji.medium.com/kubernetes-policy-as-code-kyverno-vs-opa-e44e0d613d8a |

---

### Long tail — policy-as-code

| Tool | URL | Noot |
|------|-----|------|
| **Conftest** | https://github.com/open-policy-agent/conftest | Apache-2.0; OPA sub-project; test structured config (YAML/JSON/HCL/Terraform) tegen Rego-policies in CI/CD; uitstekend als pre-commit/pipeline-gate. |
| **Checkov** | https://github.com/bridgecrewio/checkov | Apache-2.0; Terraform/Kubernetes/CloudFormation IaC security scanner; gemakkelijk in CI/CD; door Palo Alto overgenomen maar kern blijft open source. |

---

## Niet-gedekt / gaps

De volgende gebieden vallen binnen PROTECT maar zijn in dit onderzoek **niet of onvoldoende gedekt** door beschikbare open-source tooling:

1. **Data-beveiliging (PR.DS) — DLP/data discovery**: Geen rijpe, volledig open-source DLP-oplossing gevonden. Commerciële markt domineert. Partieel gedekt door Wazuh (file integrity) en OpenDLP (oud, nauwelijks onderhouden). **Gap: hoog.**

2. **Platform security voor Windows/macOS (PR.IP)**: OpenSCAP ondersteunt Windows officieel niet meer (vervallen feb 2022). Lynis is Unix-only. Windows-hardening via Microsoft DSC (niet open source) of Ansible Windows-rollen (dev-sec in progress). **Gap: matig.**

3. **Network access control / microsegmentatie (PR.AC)**: Open-source NAC-oplossingen (PacketFence) bestaan maar zijn complex; niet in dit onderzoek meegenomen. **Gap: matig.**

4. **Secrets management (PR.AC)**: HashiCorp Vault (BSL-licentie ⚠️ — source-available, niet OSI-open since aug 2023) en OpenBao (MPL-2.0, community fork) bestaan. OpenBao als OSS-alternatief verdient een apart onderzoek. **Licentiewaarschuwing: Vault is GEEN open source meer.**

5. **Security awareness-content**: Open-source SCORM-inhoud voor security awareness is schaars; Moodle als LMS is solide maar organisaties zijn afhankelijk van externe content-pakketten (veelal commercieel) of zelf bouwen. **Gap: inhoud, niet tooling.**

6. **Privileged Access Management (PAM)**: Geen volledig open-source PAM-suite gevonden die enterprise-ready is. Teleport (Apache-2.0 community) en Boundary (BSL ⚠️) zijn kandidaten; Teleport verdient apart onderzoek. **Gap: matig.**

---

## Licentie-waarschuwingen (samenvatting)

| Tool | Claim | Werkelijkheid |
|------|-------|---------------|
| HashiCorp Vault | "Open source" | ⚠️ **BSL 1.1** (source-available) since aug 2023 — GEEN OSI-open source. Gebruik OpenBao als fork. |
| CIS-CAT (Lite/Pro) | "Gratis tool" | ⚠️ **Proprietary** — geen open source. |
| Zitadel v3+ | "Open source" | ✅ maar **AGPL-3.0** (copyleft) — modificaties moeten openbaar; commerciële licentie beschikbaar. |
| Phishing Frenzy | "Open source" | ✅ GPL maar **project inactief** — veiligheidsbezwaren. |
| Gophish | "Actief OSS" | ✅ MIT maar **geen releases sinds sept 2022** — onderhoudszorg. |

---

*Peildatum: juni 2026. Bronnen geverifieerd via GitHub-repo's en bronartikelen. Alle licentie-claims gebaseerd op LICENSE-bestanden in officiële repositories.*
