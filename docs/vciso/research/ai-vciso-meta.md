# AI & Open-Source (v)CISO-Ondersteuning — Meta-onderzoek
**Scope:** Open-source projecten die de rol van een (v)CISO geheel of deels nabootsen of ondersteunen
met AI/LLM/agents. Ordeningsframe: NIST CSF 2.0 (Govern · Identify · Protect · Detect · Respond · Recover).
**Peildatum:** juni 2026. **Filter:** OSI-erkende open-source licenties; source-available licenties (BSL/SSPL/ELv2/CC-NC) apart geflagged.

---

## Uitgewerkte Projecten

---

### 1. CISO Assistant Community Edition
**URL:** https://github.com/intuitem/ciso-assistant-community

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Govern ●●● · Identify ●●● · Protect ●● · Detect ○ · Respond ○ · Recover ○ |
| **Capability** | Full-stack GRC-platform: risk management, compliance/audit, AppSec, TPRM, BIA, privacy, reporting |
| **Omschrijving** | One-stop-shop GRC-platform van Intuitem, ondersteunt 150+ frameworks (ISO 27001, NIST CSF, NIS2, DORA, EU AI Act, NIST AI RMF, PCI DSS, SOC 2, CMMC en meer) met automatische control-mapping. Community-editie is volledig zelfgehost. Bevat een ingebouwde chat-module met configureerbare lokale LLM-engine, plus MCP-integratie voor externe toolkoppelingen. |
| **Rijpheid** | ●●●●○ — 4,1k stars, 747 forks, 272 releases (laatste: v3.18.1 op 15 juni 2026), actief onderhouden |
| **Licentie** | AGPL-3.0 (community). ⚠️ Enterprise-functies in `/enterprise`-directory zijn proprietary. |
| **EU-soevereiniteit** | ✅ Volledig zelfhostbaar, Franse vendor (Intuitem), geen SaaS-afhankelijkheid vereist |
| **Integreerbaarheid** | API-first (REST + Swagger), MCP Registry vermeld, webhooks. Django/Python-backend + SvelteKit-frontend |
| **AI-native koppeling** | ●●●○○ — lokale LLM-engine (backend/chat-module), MCP-support, geen agentic workflow out-of-the-box |
| **Stack** | Python (Django) · SvelteKit/TypeScript · PostgreSQL/SQLite · Docker |
| **Fit-score** | **5/5** — rijpste open-source GRC-platform, hoogste framework-breedte, meest geschikte bouwsteen voor de dirigent als compliance-ruggengraat |
| **Bronnen** | https://github.com/intuitem/ciso-assistant-community · https://intuitem.gitbook.io/ciso-assistant · https://www.helpnetsecurity.com/2026/01/14/ciso-assistant-open-source-cybersecurity-management-grc/ |
| **CSF-dekking** | Govern (risk register, beleid, frameworks) en Identify (asset context, gap-analyse, TPRM) zijn primair. Protect via AppSec-module. Detect/Respond/Recover niet gedekt. |
| **Aanpak** | Workflow + rule-based control-mapping; LLM/RAG in ontwikkeling (chat-module aanwezig, RAG gepland) |
| **Herbruikbaarheid** | Framework-library (150+ frameworks als YAML/JSON), control-mapping engine, en TPRM-module direct herbruikbaar als kennislaag voor onze dirigent. Het dossier-register-concept in ATLAS spiegelt de CISO Assistant-structuur. Overweeg MCP-koppeling als compliance-backend. |

---

### 2. AiSOC — AI-powered Security Operations Center
**URL:** https://github.com/beenuar/AiSOC

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Detect ●●● · Respond ●●● · Identify ●● · Recover ● · Govern ● · Protect ○ |
| **Capability** | Autonome SOC: alert-fusie, multi-agent triage, threat hunting, SOAR-automatisering, compliance-evidence |
| **Omschrijving** | Zelfhostbaar MIT-gelicentieerd SOC-platform met LangGraph multi-agent orchestrator. Vier primaire agents (DetectAgent, TriageAgent, HuntAgent, RespondAgent) met drielaagse geheugenstructuur (sessie, werkgeheugen, institutioneel). Bevat RAG op MITRE ATT&CK via Qdrant. 800+ Sigma-regels, 50+ connectors (CrowdStrike, Splunk, Sentinel, Okta, AWS Security Hub). Compliance-coverage voor SOC 2, ISO 27001, NIST CSF, PCI-DSS, HIPAA, DORA. Volledig auditeerbaar: Investigation Ledger logt elke LLM-prompt, toolaanroep en evidentiebron. |
| **Rijpheid** | ●●●●○ — 1,4k stars, 140 forks, v7.4.0 (29 mei 2026), 379+ commits, publieke eval-harness met 200-incident corpus |
| **Licentie** | MIT ✅ |
| **EU-soevereiniteit** | ✅ Volledig zelfhostbaar, airgap-modus beschikbaar (Ollama sidecar, geen externe feeds) |
| **Integreerbaarheid** | OpenAPI 3.1 + GraphQL + REST, SDK voor TypeScript/Python/Go, plugin SDK, MCP-protocol-support |
| **AI-native koppeling** | ●●●●● — LangGraph-native, RAG (Qdrant), multi-agent, Kafka event spine, per-decisie confidence-thresholds |
| **Stack** | Python · TypeScript · PostgreSQL · Kafka · Qdrant · Docker/Kubernetes |
| **Fit-score** | **4/5** — sterkste open-source SOC-agent; mist GRC/governance-laag maar heeft de rijkste orchestratie-architectuur |
| **Bronnen** | https://github.com/beenuar/AiSOC |
| **CSF-dekking** | Detect en Respond dominant (full-stack SOC); Identify partieel (asset/identity-context via connectors); Govern beperkt (RBAC, RBAC, audit-log, compliance-mapping aanwezig maar geen risk register) |
| **Aanpak** | Multi-agent (LangGraph) + RAG (Qdrant/MITRE ATT&CK) + workflow (Kafka) + HITL-goedkeuringspoorten |
| **Herbruikbaarheid** | Investigation Ledger-patroon (elke AI-beslissing auditeerbaar) direct toepasbaar op dirigent. Drielaagse geheugenarchitectuur (sessie/werkgeheugen/institutioneel) is een blauwdruk voor onze context-management. Confidence-threshold-gates = operationalisering van de noorderster. |

---

### 3. Prowler — Cloud Security Platform met Lighthouse AI
**URL:** https://github.com/prowler-cloud/prowler

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Identify ●●● · Detect ●●● · Govern ●● · Protect ●● · Respond ● · Recover ○ |
| **Capability** | Cloud security posture management (CSPM), compliance-scanning, AI-aangedreven remediation via MCP |
| **Omschrijving** | "World's most widely used open-source cloud security platform" (14k stars). Automatiseert security- en compliance-checks over AWS, Azure, GCP en meer. Ondersteunt NIST CSF, ISO 27001, CIS, NIST 800, MITRE ATT&CK, NIS2, GDPR, HIPAA, PCI DSS, SOC 2, BSI C5 en tientallen andere frameworks. Lighthouse AI (MCP-server) biedt een AI-gedreven security-assistent die misconfiguraties detecteert, risico's beoordeelt en automatisch remediation-pull-requests aanmaakt. Integreert in Cursor, Claude Code en VS Code. |
| **Rijpheid** | ●●●●● — 14k stars, v5.30.2 (17 juni 2026), Apache 2.0, jarenlange productie-adoptie |
| **Licentie** | Apache 2.0 ✅ (core CLI + checks). Prowler Cloud = commerciële SaaS-laag, niet vereist. |
| **EU-soevereiniteit** | ✅ CLI volledig lokaal/zelfhostbaar. Lighthouse MCP werkt lokaal. Prowler Cloud is optionele US-hosted SaaS (⚠️ als gebruikt: EU-soevereiniteitscheck vereist). |
| **Integreerbaarheid** | MCP-server (Lighthouse), CLI/CI-CI-friendly, Python API, GitHub Actions marketplace |
| **AI-native koppeling** | ●●●●○ — MCP-native, LLM-aangedreven remediation, AI skills voor coding-assistenten |
| **Stack** | Python · Docker · MCP |
| **Fit-score** | **4/5** — onmisbaar voor Identify/Detect op cloudinfrastructuur; beperkt in governance/risicolaag |
| **Bronnen** | https://github.com/prowler-cloud/prowler · https://prowler.com/blog/prowler-launches-lighthouse-ai-and-mcp-server-bringing-autonomous-security-to-devsecops-teams · https://docs.prowler.com/getting-started/installation/prowler-mcp |
| **CSF-dekking** | Identify (asset-inventaris, misconfiguratie-detectie, compliance-gap) en Detect (continuous monitoring) zijn sterk. Govern via framework-rapportage. Protect via beleidsbewaking. |
| **Aanpak** | Rule-based checks + AI-agent (Lighthouse MCP) + workflow-automatisering |
| **Herbruikbaarheid** | MCP-server-patroon (Lighthouse) toont hoe je een bestaand security-tool-domein via MCP aan een LLM-dirigent koppelt zonder de tool te herschrijven. Direct herbruikbaar als Identify/Detect-module. |

---

### 4. Microsoft Agent Governance Toolkit
**URL:** https://github.com/microsoft/agent-governance-toolkit

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Govern ●●● · Protect ●●● · Identify ●● · Detect ●● · Respond ● · Recover ○ |
| **Capability** | Runtime governance voor autonome AI-agents: policy enforcement, zero-trust identity, execution sandboxing, audit trails |
| **Omschrijving** | Microsoft-toolkit die alle 10 OWASP Agentic AI Top 10 risico's (2026) deterministisch afdekt. Zeven modulaire packages: Agent OS (policy engine YAML/OPA/Cedar, <0,1ms p99), Agent Mesh (SPIFFE/DID/mTLS identiteit), Agent Runtime (privilege rings), Agent SRE (SLOs, circuit breakers), Agent Compliance (governance-verificatie), Agent Marketplace (plugin-signing), Agent Lightning (RL-trainingsgovernance). Niet een CISO-tool in de klassieke zin, maar de governance-laag die nodig is zodra de dirigent zelf autonoom handelt. Compliance-mapping naar NIST AI RMF, EU AI Act, SOC 2, OWASP. |
| **Rijpheid** | ●●●●○ — 4,4k stars, 620 forks, v4.1.0 (9 juni 2026), 2.101 commits, 19 releases |
| **Licentie** | MIT ✅ |
| **EU-soevereiniteit** | ✅ Volledig lokaal deploybaar; EU AI Act-mapping aanwezig |
| **Integreerbaarheid** | Framework-adapters voor OpenAI Agents, CrewAI, LangGraph, Semantic Kernel, AutoGen; Python/TypeScript/.NET/Rust/Go |
| **AI-native koppeling** | ●●●●● — ontworpen specifiek als governance-laag voor AI-agents; MCP Security Gateway ingebouwd |
| **Stack** | Python · TypeScript · .NET · Rust · Go · OPA/Cedar · SPIFFE |
| **Fit-score** | **4/5** — cruciale bouwsteen voor noorderster-implementatie in de dirigent; geen GRC-inhoud, wel de governance-mechanismen |
| **Bronnen** | https://github.com/microsoft/agent-governance-toolkit · https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit-open-source-runtime-security-for-ai-agents/ |
| **CSF-dekking** | Govern (policy enforcement, audit trails, compliance-mapping) en Protect (identity, sandboxing, tool-poisoning-detectie) zijn dominant. Detect via MCP Security Gateway en PromptDefense. |
| **Aanpak** | Rule-based policy enforcement (deterministisch, niet probabilistisch) + identity mesh + audit-log |
| **Herbruikbaarheid** | Policy-as-code patroon (YAML/OPA) voor het bewaken van agentic acties is direct toepasbaar op de routing-gate en noorderster in ATLAS. Tamper-evident Merkle audit trail = blauwdruk voor decisions/log. MCP Security Gateway beschermt tool-aanroepen van de dirigent. |

---

### 5. STRIDE-GPT
**URL:** https://github.com/mrwadams/stride-gpt

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Identify ●●● · Govern ●● · Protect ●● · Detect ○ · Respond ○ · Recover ○ |
| **Capability** | AI-gedreven threat modeling (STRIDE, DREAD, MITRE ATT&CK, OWASP LLM/Agentic Top 10) |
| **Omschrijving** | LLM-tool voor geautomatiseerde threat modeling. Gebruiker beschrijft applicatie; het systeem genereert STRIDE-bedreigingen, attack trees, DREAD-scores en mitigaties. Agentic workflow: planning → per-subsysteem exploratie → synthesepass. Ondersteunt OWASP LLM Top 10, OWASP ASI Top 10 (agentic AI), MITRE ATT&CK/ATLAS. Output in Markdown, JSON, SARIF, HTML en Mermaid-diagrammen. Ondersteunt GPT-5, Claude 4.5, Gemini 3, Mistral, Groq en lokale modellen (LM Studio). |
| **Rijpheid** | ●●●●○ — 1,1k stars, 307 forks, v0.17+, 242+ commits, actieve CI met CodeQL/Bandit/Trivy/Gitleaks |
| **Licentie** | MIT ✅ |
| **EU-soevereiniteit** | ✅ Draait lokaal (CLI, Docker); ondersteunt lokale LLM-inferentie via LM Studio |
| **Integreerbaarheid** | CLI (`pip install stride-gpt`), Streamlit web UI, Docker, SARIF-output voor IDE/GitHub-integratie |
| **AI-native koppeling** | ●●●●○ — agentic workflow, multi-model routing (architect + worker), extended thinking support |
| **Stack** | Python · Streamlit · Docker |
| **Fit-score** | **4/5** — beste open-source LLM-threat-modeler; Identify-scharnierpunt in de dirigent |
| **Bronnen** | https://github.com/mrwadams/stride-gpt |
| **CSF-dekking** | Identify (threat modeling, risicobeoordeling) is dominant. Govern partieel via beleidsdocumentatie-output. Protect via mitigatie-aanbevelingen. |
| **Aanpak** | Agentisch (planning + exploratie + synthese) + multi-model routing + rule-based framework-mapping |
| **Herbruikbaarheid** | Twee-tier model-routing (architect/worker) is een efficiënt patroon voor onze dirigent. SARIF-output biedt machineleesbare bevindingen die direct in een GRC-backend (bv. CISO Assistant) kunnen landen. Subsysteem-per-subsysteem exploratiepatroon is een blauwdruk voor scope-afbakening in risicoanalyse-agents. |

---

### 6. ITBench CISO-CAA Agent (IBM Research)
**URL:** https://github.com/itbench-hub/ITBench-CISO-CAA-Agent

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Govern ●●● · Identify ●●● · Protect ●● · Detect ● · Respond ○ · Recover ○ |
| **Capability** | Compliance-assessment-automatisering: natural-language naar policy (Kyverno/OPA Rego), evidence-collectie, GitOps-integratie |
| **Omschrijving** | IBM Research-project dat CISO-agents bouwt voor geautomatiseerde compliance-assessments op Kubernetes-omgevingen. Genereert policies vanuit natural language, verzamelt evidence automatisch en deployt via GitOps. Gebouwd op CrewAI + LangGraph + LiteLLM (multi-LLM: IBM watsonx.ai, OpenAI, Azure). Onderdeel van het ITBench-benchmarkframework (ICML 2025, Oral). Benchmark-resultaat: agents lossen 25,2% van CISO-scenario's op (state-of-the-art modellen, juni 2025). |
| **Rijpheid** | ●●○○○ — 20 stars, 8 forks, vroeg stadium, maar gegrond in peer-reviewed onderzoek (arXiv:2502.05352, ICML 2025) |
| **Licentie** | Apache 2.0 ✅ |
| **EU-soevereiniteit** | ✅ Zelfhostbaar via Docker/Podman; LiteLLM maakt lokale modellen mogelijk |
| **Integreerbaarheid** | Kubernetes-native (Kyverno/OPA Rego deployment), Docker/Podman |
| **AI-native koppeling** | ●●●●○ — multi-agent (CrewAI + LangGraph), multi-LLM via LiteLLM, gestructureerde taakflows |
| **Stack** | Python · CrewAI · LangGraph · LiteLLM · Docker |
| **Fit-score** | **3/5** — wetenschappelijk fundament en agent-patronen waardevol; te vroeg voor productie; Kubernetes-focus beperkt bredere toepassing |
| **Bronnen** | https://github.com/itbench-hub/ITBench-CISO-CAA-Agent · https://arxiv.org/abs/2502.05352 · https://proceedings.mlr.press/v267/jha25a.html |
| **CSF-dekking** | Govern (compliance-beleid genereren en deployen) en Identify (evidence-collectie, control-verificatie) zijn gedekt. Protect partieel via policy-enforcement op cluster. |
| **Aanpak** | Multi-agent (CrewAI + LangGraph) + tool-using agents + GitOps-workflow |
| **Herbruikbaarheid** | Natural-language → gestructureerde policy-output (Kyverno/OPA) is een concreet patroon voor de "beleidsgenerator"-component van de dirigent. Benchmark-methodiek (25,2% oplosratio) geeft realistische verwachtingen voor agentic compliance-automatisering. |

---

### 7. NVISO Cyber-Security LLM Agents
**URL:** https://github.com/NVISOsecurity/cyber-security-llm-agents

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Detect ●●● · Respond ●● · Protect ● · Identify ● · Govern ○ · Recover ○ |
| **Capability** | EDR-detectie-engineering, CI/CD-security-automatisering, endpoint-security-assessments |
| **Omschrijving** | Collectie LLM-agents voor dagelijkse cybersecurity-taken. Gepresenteerd op RSAC 2024 (EDR-evasion + detection engineering). Modulaire aanpak: individuele agents + taken die gecombineerd worden tot workflows. Gebouwd op Microsoft AutoGen. Primair Jupyter Notebook / Python. Vroeg stadium, disclaimers over breaking changes. |
| **Rijpheid** | ●●●○○ — 370 stars, 70 forks, "early stages of development" (eigen disclaimer) |
| **Licentie** | GPL-3.0 ✅ (let op: copyleft — afgeleid werk moet ook GPL zijn) |
| **EU-soevereiniteit** | ✅ Zelfhostbaar; OpenAI API afhankelijkheid (⚠️ vervangbaar via AutoGen multi-LLM) |
| **Integreerbaarheid** | AutoGen-gebaseerd, Jupyter Notebook-workflows, Python |
| **AI-native koppeling** | ●●●○○ — AutoGen multi-agent, modulaire taakflows, tool-using |
| **Stack** | Python · Jupyter Notebook · Microsoft AutoGen |
| **Fit-score** | **3/5** — goede blauwdruk voor detection engineering-automatisering; te vroeg voor productie |
| **Bronnen** | https://github.com/NVISOsecurity/cyber-security-llm-agents |
| **CSF-dekking** | Detect (EDR-analyse, detection engineering) en Respond (CICD-integratie, geautomatiseerde respons) zijn primair. |
| **Aanpak** | Multi-agent (AutoGen) + werkstroomautomatisering + tool-using |
| **Herbruikbaarheid** | "Batteries included"-aanpak (kant-en-klare workflows voor specifieke taken) is een bruikbaar ontwerppatroon. Modulaire agent+taak-compositie toont hoe je specialistische security-kennis opdeelt in herbruikbare bouwstenen. |

---

### 8. Anthropic Cybersecurity Skills
**URL:** https://github.com/mukul975/Anthropic-Cybersecurity-Skills

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Govern ●●● · Identify ●●● · Protect ●●● · Detect ●●● · Respond ●●● · Recover ●● |
| **Capability** | Kennisbank van 754 gestructureerde cybersecurity-skills voor AI-agents, gemapped op 5 frameworks |
| **Omschrijving** | Open-source skills-bibliotheek (agentskills.io-standaard) met 754 skills over 26 security-domeinen (inclusief Compliance & Governance, Threat Hunting, IR, Cloud Security, IAM, enz.). Elke skill heeft YAML-frontmatter (~30 tokens) voor snelle ontdekking en volledige Markdown-workflow (~500–2.000 tokens). Gemapped op MITRE ATT&CK v19.1 (286 technieken), NIST CSF 2.0 (alle 6 functies), MITRE ATLAS v5.4, D3FEND v1.3, NIST AI RMF 1.0. Compatibel met Claude Code, GitHub Copilot, Cursor, LangChain, CrewAI, AutoGen en 20+ platforms. |
| **Rijpheid** | ●●●●● — 16,1k stars, 2k forks, v1.2.0 (6 april 2026) |
| **Licentie** | Apache 2.0 ✅ |
| **EU-soevereiniteit** | ✅ Statische kennisbank, geen SaaS-afhankelijkheid |
| **Integreerbaarheid** | `npx skills add` CLI-installatie; universeel (elke agent-runtime die YAML/Markdown leest) |
| **AI-native koppeling** | ●●●●● — ontworpen voor agent-runtime integratie; progressive disclosure (frontmatter → volledige workflow) optimaliseert token-gebruik |
| **Stack** | YAML · Markdown (agnostic) |
| **Fit-score** | **5/5** — uniek als framework-agnostische kennislaag voor de dirigent; hoogste star-count in deze categorie |
| **Bronnen** | https://github.com/mukul975/Anthropic-Cybersecurity-Skills |
| **CSF-dekking** | Volledige breedte over alle 6 CSF-functies; diepte varieert per domein maar CSF 2.0-mapping is expliciet gedocumenteerd |
| **Aanpak** | Kennisrepresentatie (geen agent-runtime zelf) — structured skills als prompt-context voor agent-beslissingen |
| **Herbruikbaarheid** | Progressive disclosure-patroon (frontmatter scouting → volledige skill laden op match) is dé blauwdruk voor token-efficiënte kennisloading in de dirigent. Skill-structuur (When to Use · Prerequisites · Workflow · Verification) is direct te hergebruiken als taaktemplate. |

---

### 9. Admyral — Continuous Control Monitoring
**URL:** https://github.com/Hey-Telo/admyral

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Govern ●●● · Identify ●● · Protect ●● · Detect ●● · Respond ● · Recover ○ |
| **Capability** | Workflow-gebaseerde GRC-automatisering: control-monitoring, evidence-collectie, LLM-acties |
| **Omschrijving** | Open-source platform voor continue control monitoring met Python SDK en no-code drag-and-drop workflow-builder (bidirectionele sync met code). Gebaseerd op Temporal (Netflix) voor betrouwbare werkstromen. Ondersteunt LLM-acties via OpenAI, Mistral, Anthropic voor taken als bevindingen samenvatten, rapportgeneratie en alertcategorisering. |
| **Rijpheid** | ●●●○○ — 340 stars, 19 forks, 873 commits, actief onderhouden |
| **Licentie** | Apache 2.0 ✅ |
| **EU-soevereiniteit** | ✅ Zelfhostbaar (Docker); LLM-keuze configureerbaar (Mistral-lokaal mogelijk) |
| **Integreerbaarheid** | Python SDK + no-code UI, Temporal-backend, REST API |
| **AI-native koppeling** | ●●●○○ — LLM-acties als workflow-stap; geen native multi-agent orchestratie |
| **Stack** | Python · TypeScript/Next.js · Temporal · PostgreSQL · Docker |
| **Fit-score** | **3/5** — solide voor GRC-workflow-automatisering; minder rijp dan CISO Assistant voor framework-compliance |
| **Bronnen** | https://github.com/Hey-Telo/admyral |
| **CSF-dekking** | Govern (control-monitoring, evidence) en Identify (control-inventarisatie) zijn primair; Protect/Detect via workflow-integraties |
| **Aanpak** | Workflow-gebaseerd (Temporal) + LLM-acties als stap; hybride |
| **Herbruikbaarheid** | "Controls as code" patroon (Python SDK met no-code UI) is een interessante brug tussen technische en niet-technische gebruikers. Temporal-gebaseerde betrouwbaarheidsgaranties zijn relevant voor de dirigent-betrouwbaarheidslaag. |

---

### 10. NIST CSF 2.0 MCP Server
**URL:** https://github.com/rocklambros/nist-csf-2-mcp-server

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Govern ●●● · Identify ●●● · Protect ● · Detect ○ · Respond ○ · Recover ○ |
| **Capability** | 40 MCP-tools voor NIST CSF 2.0 assessment, gap-analyse, executive reporting en voortgangsregistratie |
| **Omschrijving** | Open-source MCP-server die het volledige NIST CSF 2.0 model (6 functies, 23 categorieën, 106 subcategorieën) blootlegt als AI-tools. 740 assessment-vragen, gap-analyse, prioriteringsmatrices, executive rapportage, compliance-mapping, voortgangsregistratie. <100ms responstijden, REST + WebSocket + MCP. Professionele PDF-export. Persistent assessment-sessies (pause/resume). |
| **Rijpheid** | ●●●○○ — 62 stars, actieve ontwikkeling, 145 open issues, MIT-licentie |
| **Licentie** | MIT ✅ |
| **EU-soevereiniteit** | ✅ Volledig lokaal (Docker/Kubernetes); geen externe afhankelijkheden vereist |
| **Integreerbaarheid** | MCP-native, REST + WebSocket, Docker, Kubernetes/Helm |
| **AI-native koppeling** | ●●●●○ — ontworpen als MCP-server voor AI-assistenten; Claude/OpenAI-compatibel |
| **Stack** | TypeScript/Node.js · HTML · Docker |
| **Fit-score** | **3/5** — focust en laag sterren maar unieke waarde als NIST CSF 2.0 MCP-bouwsteen; nog niet productierijp |
| **Bronnen** | https://github.com/rocklambros/nist-csf-2-mcp-server · https://www.rockcybermusings.com/p/nist-csf-20-mcp-server-shipping-an |
| **CSF-dekking** | Govern en Identify volledig (alle 106 subcategorieën bereikbaar); Protect partieel via framework-crosswalks |
| **Aanpak** | MCP tool-server (39–40 tools) + SQLite-persistentie + rule-based framework-evaluatie |
| **Herbruikbaarheid** | Directe "plug-in" voor een AI-dirigent die NIST CSF-assessments moet uitvoeren. Toont het patroon van een framework-kennisbank als MCP-server — herhaalbaar voor ISO 27001, NIS2, DORA etc. |

---

### 11. SOCFortress CoPilot
**URL:** https://github.com/socfortress/CoPilot

| Veld | Waarde |
|------|--------|
| **CSF-functies** | Detect ●●● · Respond ●●● · Identify ●● · Govern ● · Protect ○ · Recover ○ |
| **Capability** | Single-pane-of-glass voor open-source SIEM-stack (Wazuh, Graylog, Velociraptor, Grafana), MCP-interface |
| **Omschrijving** | Open-source beveiligingsplatform dat Wazuh, Graylog, Velociraptor, Grafana en InfluxDB integreert in één UI. MCP-service maakt natural-language queries over de volledige stack mogelijk. Gericht op het verlagen van de drempel voor open-source security-tooling. Beta-fase (v0.1.74, 16 juni 2026). |
| **Rijpheid** | ●●●○○ — 498 stars, 131 forks, 84 releases, 1.000+ commits, beta-status |
| **Licentie** | AGPL-3.0 ✅ (let op: copyleft) |
| **EU-soevereiniteit** | ✅ Volledig zelfhostbaar; geen externe AI-afhankelijkheid vereist |
| **Integreerbaarheid** | MCP-service, REST API, Python/Vue/TypeScript-stack |
| **AI-native koppeling** | ●●●○○ — MCP-interface aanwezig; AI-acties beperkt beschreven in beschikbare docs |
| **Stack** | Python · Vue · TypeScript · Docker |
| **Fit-score** | **3/5** — goede integratiehub voor open-source SOC-tooling; beta; MCP-laag is interessant als orkestratie-interface |
| **Bronnen** | https://github.com/socfortress/CoPilot · https://socfortress.medium.com/ai-agent-for-your-open-source-siem-stack-is-here-wazuh-velociraptor-and-copilot-just-got-2e0542aac697 |
| **CSF-dekking** | Detect en Respond (SOC-operaties) dominant; Identify via asset-context van Wazuh/Velociraptor |
| **Aanpak** | Integratiehub + MCP tool-server; LLM-acties via MCP-interface |
| **Herbruikbaarheid** | MCP-als-SIEM-interface-patroon: toont hoe je meerdere tools via één MCP-server samenvoegt voor de dirigent. |

---

## Long Tail — Marginale of Vroegstadium Projecten

| Naam | URL | Status / 1 zin |
|------|-----|----------------|
| Agentic SOC Platform (FunnyWolf) | https://github.com/FunnyWolf/agentic-soc-platform | MIT · 897 stars · LLM-gegenereerde incidentrapporten + SIEM-integratie; primair SOC Detect/Respond, geen GRC |
| GigaChad-GRC | https://github.com/grcengineering/gigachad-grc | ⚠️ **Elastic License 2.0 (NIET-OSI)** · 136 stars · GRC-platform met AI risk scoring; bruikbaar intern, niet als OSS beschouwd |
| VerifyWise | https://github.com/verifywise-ai/verifywise | ⚠️ **BSL 1.1 (NIET-OSI)** · 310 stars · AI-governance voor EU AI Act/ISO 42001; source-available, geen OSS |
| Cybersecurity AI (CAI / aliasrobotics) | https://github.com/aliasrobotics/cai | ⚠️ AGPL + MIT dubbel · 9,2k stars · Offensief/defensief AI-framework; geen GRC/governance-functies |
| NVISO LLM-threat-modeling (Jupyter/Neo4j) | https://github.com/castlebbs/llm-threat-modeling | MIT · lage stars · Threat-modeling via Neo4j + Claude; OWASP Dublin 2025-presentatie; proof-of-concept |
| UniCIS Platform CE | https://github.com/UnicisTech/unicis-platform-ce | MIT · 93 stars · GRC-alternatief voor Vanta/Drata; geen AI-features; TypeScript |
| Probo | https://github.com/getprobo/probo | MIT · 1,2k stars · SOC2/GDPR/ISO 27001; geen LLM/AI; Go |
| Comply (StrongDM) | https://github.com/strongdm/comply | MIT · 1,6k stars · SOC 2 compliance-as-code; geen AI; oudere repo |
| Ansvar-Systems/security-controls-mcp | https://github.com/Ansvar-Systems/security-controls-mcp | Onbekende licentie · 28 frameworks (ISO 27001, NIST CSF 2.0, IEC 62443); veelbelovend MCP-project, te vroeg |
| Ansvar-Systems/EU_compliance_MCP | https://github.com/Ansvar-Systems/EU_compliance_MCP | Onbekende licentie · EU-gerichte compliance MCP-server; te vroeg |
| fr33d3m0n/threat-modeling | https://github.com/fr33d3m0n/threat-modeling | MIT · LLM-native threat modeling skill voor Claude Code; vroeg stadium |
| xvnpw/ai-threat-modeling-action | https://github.com/xvnpw/ai-threat-modeling-action | MIT · GitHub Action voor AI-threat-modeling; **deprecated** |
| CPAtoCybersecurity/csf_profile | https://github.com/CPAtoCybersecurity/csf_profile | MIT · 41 stars · NIST CSF-assessmenttool (geen AI); bruikbaar als referentie |
| KunalCyber/GRC-Prompts-Library | https://github.com/KunalCyber/GRC-Prompts-Library | Apache 2.0 · 10 stars · Productie-GRC-prompts voor 13 domeinen incl. EU AI Act, ISO 27001; promptbibliotheek |
| ethanolivertroy/flue-grc-engineer-demo | https://github.com/ethanolivertroy/flue-grc-engineer-demo | MIT · 2 stars · GRC-agent demo op Cloudflare Workers + Workers AI; POC |
| ITBench (IBM benchmark) | https://github.com/itbench-hub/ITBench | Apache 2.0 · Benchmarkframework (niet een productietool); waardevol voor evaluatie van agent-capaciteiten |
| tnicholson/nist-mcp-server | https://github.com/tnicholson/nist-mcp-server | Onbekend · NIST-analyse MCP-server; lage adoptie |
| mcp-security-standard/mcp-server-security-standard | https://github.com/mcp-security-standard/mcp-server-security-standard | Apache 2.0 · Open MCP-beveiligingsstandaard (MSSS); normatief document, geen tool |

---

## Lessen voor de Dirigent-Architectuur

Dit is de kernleverantie: concrete patronen en valkuilen die het cisochat-orkestratie-ontwerp informeren.

### Patroon 1: Gelaagde geheugenarchitectuur (AiSOC-blauwdruk)
AiSOC's drielaagse geheugen (sessie / werkgeheugen / institutioneel) is de rijpste implementatie van context-management in een security-agent. De dirigent moet dit onderscheid expliciet maken: wat vergeet hij na de sessie, wat houdt hij bij per case, en wat kristalliseert als institutionele kennis in de wiki-laag? De huidige `_VOLGENDE-KEER.md`-structuur in ATLAS is een rudimentaire versie hiervan; de agent-architectuur heeft een formeler model nodig.

### Patroon 2: Progressive disclosure voor token-efficiëntie (Anthropic Cybersecurity Skills)
De agentskills.io-aanpak — YAML-frontmatter (~30 tokens) voor ontdekking, volledige workflow (~500–2.000 tokens) on-demand laden — is dé oplossing voor de trade-off tussen breedte en diepte in de dirigent. Implementeer skills als twee-laags bestanden: routing-header (klein) + uitvoeringsprotocol (groot). Laad de tweede laag alleen als de eerste matcht.

### Patroon 3: MCP als domein-interface (Prowler Lighthouse + NIST CSF MCP Server)
Elk security-domein heeft zijn eigen tool-universe. MCP-servers zijn de juiste abstraktielaag: ze kapselen domein-specifieke tools (Wazuh, Prowler, NIST CSF-framework) in en bieden een uniforme interface voor de dirigent. Bouw geen monolithische agent — bouw een dirigent die MCP-servers voor Identify (Prowler), Detect (AiSOC/CoPilot), GRC (CISO Assistant) en Govern (AGT) aanstuurt.

### Patroon 4: Deterministisch policy enforcement, niet probabilistisch (Microsoft AGT)
De fundamentele les van het Agent Governance Toolkit: LLM-gebaseerde guardrails falen onder adaptieve aanvallen (100% aanvalsratio op GPT-4o, Claude 3, Llama-3). Verboden acties moeten *structureel onmogelijk* zijn (application-layer interception vóór tool-uitvoering), niet afhankelijk van het model dat "nee" zegt. Dit is de technische implementatie van de noorderster: de routing-gate moet deterministische policy checks bevatten, geen LLM-gebaseerde zelfreflectie.

### Patroon 5: Audit-by-design met Investigation Ledger (AiSOC)
Elke LLM-prompt, toolaanroep, evidentiebron en beslissing moet gelogd worden in een tamper-evident audit trail (AiSOC's Investigation Ledger / AGT's Merkle-audit). Dit is niet alleen good practice — het is de technische implementatie van "auditbaar by design" uit het ATLAS-operating manual. De `decisions/log` in ATLAS is het semantische equivalent; de dirigent-architectuur heeft een machineleesbare variant nodig.

### Patroon 6: Benchmark-gegronde verwachtingen (ITBench)
ICML 2025: state-of-the-art modellen lossen slechts 25,2% van CISO-compliance-scenario's autonoom op. Dit is geen reden tot pessimisme maar wel een kalibratiepunt: de dirigent moet ontworpen worden als *decision support en voorbereiding*, niet als volledig autonome uitvoerder. Human-in-the-loop is niet alleen ethisch vereist (noorderster) maar ook praktisch noodzakelijk voor de huidige generatie modellen.

### Patroon 7: Composabele GRC-backbone (CISO Assistant)
CISO Assistant's 150+ framework-library met automatische control-mapping is een kant-en-klare GRC-ruggengraat. In plaats van frameworks zelf te implementeren, koppel de dirigent als frontend/agent aan CISO Assistant als backend (via MCP of REST API). Dit vermijdt de valkuil van het bouwen van een slechter GRC-systeem naast een beter bestaand systeem.

### Patroon 8: Specialisatie per CSF-functie, dirigent als orkestrator
Geen enkel project dekt alle 6 CSF-functies goed. Het landschap is:
- **Govern/Identify**: CISO Assistant (sterkst), ITBench CISO Agent, NIST CSF MCP Server
- **Identify/Detect**: Prowler Lighthouse
- **Detect/Respond**: AiSOC, SOCFortress CoPilot, Agentic SOC Platform
- **Govern (agent-runtime)**: Microsoft AGT
- **Cross-cutting kennis**: Anthropic Cybersecurity Skills

De dirigent-architectuur moet deze specialisaties respecteren: niet proberen alles zelf te doen, maar de juiste tool per CSF-functie aansturen. Dit is precies het "dirigent, geen doos"-principe.

### Valkuilen

1. **Licentie-creep**: GigaChad-GRC (ELv2) en VerifyWise (BSL 1.1) zien eruit als open source maar zijn dat niet. Check altijd op OSI-keuring. AGPL (CISO Assistant, CoPilot) vereist dat afgeleid werk ook AGPL is — relevant voor cisochat als het GRC-backend integreert.

2. **Hype vs. productierijpheid**: Veel projecten zijn POC of vroeg stadium (< 100 stars, geen releases, geen tests). De rijpste opties (CISO Assistant 4.1k, AiSOC 1.4k, AGT 4.4k, Anthropic Skills 16k) hebben bewezen community-adoptie.

3. **EU-soevereiniteit als architectuureis**: Alle uitgewerkte projecten zijn zelfhostbaar, maar sommige AI-functies (Prowler Lighthouse, AGT) leunen op externe LLM-providers (OpenAI, Azure). Zorg dat de MCP-laag model-agnostisch is en lokale modellen (Ollama, LM Studio, Mistral) ondersteunt voor soevereine deployments.

4. **25%-plafond**: De ITBench-benchmark toont dat autonome compliance-agents momenteel ~25% van echte scenario's volledig autonoom afhandelen. Schaal de dirigent-ambities dienovereenkomstig; focus op de 75% voorbereidings- en documentatietaken, niet op autonomous decision-making.

---

*Onderzoek uitgevoerd door AI-onderzoeksagent, peildatum juni 2026. Alle claims zijn geverifieerd via directe GitHub-fetch of primaire bronnen. Sterren-aantallen zijn point-in-time en kunnen fluctueren.*
