# AI-agent-security · externe bronnen (juni 2026)

> Externe, publieke bronnen over het beveiligen van AI/LLM-agents. Verzameld als grondslag voor
> de vCISO-blueprint en de redeneerlaag (RAG). Wij hosten de bronnen niet; dit zijn samenvattingen
> vanuit ons perspectief, gemapt op de NIST CSF 2.0-functies die cisochat hanteert.
> Bron: gevonden 30-06-2026, publieke LinkedIn/vendor-publicaties.

## 1. AI Security Assessment Blueprint v2.0 · Domein 02 (Context & RAG)
- **Auteur/bron:** Luis D. (aisecurityblueprint.com). Downloadbare PDF (~205 pp).
- **Essentie:** alle context is onbevestigd tot die verankerd is. Raamwerk voor veilige retrieval,
  memory-governance, prompt-injection-detectie en auditability van RAG-systemen.
- **CSF-mapping:** Protect (input/context-controle, memory-governance) · Govern (auditability).
- **Relevantie cisochat:** rechtstreeks toepasbaar op de eigen RAG-grounding (kennisbank) en op het
  toetsen van RAG-systemen die de vCISO beoordeelt.

## 2. NCC Group · "Coding Agent Security"
- **Auteur/bron:** Alex P. (NCC Group), gedeeld door Chris H. (Resilient Cyber / Zenity). Paper (~50 pp).
- **Essentie:** permission-models, sandboxing en configuratiebescherming voor coding-agents
  (Claude Code, Cursor, Codex). Aanvalsvectoren plus mitigaties.
- **CSF-mapping:** Protect (least-privilege, sandbox) · Govern (beleid op agent-tooling in dev-teams).
- **Relevantie cisochat:** governance-handvat voor CISO's die agent-gebaseerde dev-tools moeten inkaderen.

## 3. LLM multi-layer defense (defense-in-depth)
- **Auteur/bron:** Kader Mohideen ("AI x Cybersecurity").
- **Essentie:** beveiliging van LLM-applicaties moet architectureel zijn, niet bolt-on. Lagen:
  input-filtering (prompt-injection), retrieval-validatie, model-guardrails, tool-permissies
  (least privilege), output-moderatie.
- **CSF-mapping:** Protect · Detect.
- **Relevantie cisochat:** checklist om het risico van elk ingezet LLM-systeem te beoordelen,
  inclusief cisochat zelf.

## 4. Microsoft · information-flow-control & secure autonomous agents
- **Bron:** commandline.microsoft.com (via lnkd.in-redirect).
- **Essentie:** Zero Trust en data-governance voor autonome agents; informatiestroom-controle als
  ontwerpprincipe voor agent-control-flow en compliance-gates.
- **CSF-mapping:** Govern · Protect (spant in de praktijk alle functies).
- **Relevantie cisochat:** sluit aan op de EU AI Act-eisen aan cisochat zelf en aan de agents die het bestuurt.

## 5. Anthropic · "CISO's Guide to Agentic AI" (juli 2026)
- **Auteur/bron:** Jason Clinton (Deputy CISO, Anthropic). Blog, claude.com/blog/ciso-guide-to-agentic-ai.
  gevonden 23-07-2026.
- **Essentie:** maak agentic-AI-risico beheerbaar en zichtbaar i.p.v. risicovrij; laat de organisatie
  bewust risico accepteren. Vier diagnostische vragen (onvertrouwde input · actieradius · schadebereik ·
  observability), identiteits-spectrum (agent als service-account óf onder menselijke credentials — geen
  tussenvorm), zeven technische controls (IdP-integratie, connector-allowlists, per-tool-goedkeuring,
  sandboxing, egress-allowlisting, SIEM-telemetrie, kill-switches), ontwerpen op het model van over
  6 maanden, en governance zelf automatiseren met agents.
- **CSF-mapping:** Govern (risico-acceptatie, diagnostische vragen) · Protect (controls, identiteit) ·
  Detect (SIEM-telemetrie, observability).
- **Relevantie cisochat:** direct bruikbaar toetskader voor de vCISO die agentic-AI-inzet beoordeelt;
  de 7 controls en het identiteits-spectrum zijn concrete checklist-items voor `govern.md`/`protect.md`.

## 6. Elli Shlomo · "de AI-gateway is het doelwit, niet het model" (juli 2026)
- **Auteur/bron:** Elli Shlomo (Head of Security Research, Guardz; Microsoft MVP). LinkedIn-post,
  `linkedin.com/posts/elishlomo_security-cybersecurity-share-7485214715393191936-7jVm`. Geschreven vanuit
  aanvallersperspectief. gevonden 10-08-2026.
- **Essentie:** het model aanvallen is zonde van de tijd; het doelwit is de **AI-gateway**, want die bepaalt
  identiteit, tenant-context, retrieval-scope, prompt-assemblage en routing. De beschreven keten gebruikt
  geldige credentials en verstelt daarna de context die de gateway al vertrouwt: **tenant-context omhangen**
  (cross-tenant toegang tot documenten, gecachte prompts en capabilities), **prompt-versioning-poisoning**
  (een vergiftigde system-template rijdt mee op elk volgend request, verzwakt validatie en verbergt
  indicatoren), en een **endpoint-alias-swap** waardoor inferentie via het model van de aanvaller loopt
  terwijl het auditlog de goedgekeurde bestemming toont. Alles blijft er geautoriseerd uitzien.
  Kernstelling: AI-security is een **execution-integrity**-probleem, geen modelprobleem; de exploitatie zit
  in de naden tússen controls. Verdediging: bind identiteit, tenant-context, retrieval-scope, promptversie,
  modelbestemming en audit-evidence tot **één execution record**, hercontroleer vlak vóór de inference-call
  (niet alleen bij login), verifieer de destination-hash ná routing, log ook geblokkeerde en omgeleide
  requests, en fail closed bij mismatch.
- **CSF-mapping:** Protect (tenant-isolatie, promptintegriteit, routing) · Detect (destination-mismatch,
  configuratiedrift, audit-waarheid) · Identify (de gateway als control plane in beeld brengen).
- **Relevantie cisochat:** de meest concrete architectuur-checklist van de zes voor de eigen gateway-laag.
  Levert ook een kanteling voor het beoordelingskader: toets niet alleen modelrisico's maar
  execution-integrity en de betrouwbaarheid van het auditspoor ("het logboek toont wat had moeten gebeuren,
  niet wat gebeurde"). Sluit aan op audit-trail-eisen en AI threat modeling.
- **Voorbehoud:** de auteur erkent zelf twee restrisico's (agent-to-agent session smuggling; "fail closed
  helpt niet als de gatekeeper al van mij is"). Tegenwerping van Jason Keirstead in de comments: verschillende
  stappen veronderstellen feitelijk een 0-day in de gateway, dus lees dit als ontwerp-checklist, niet als
  bewezen aanvalspad.

## Rode draad
Alle zes wijzen dezelfde kant op: context/input is onvertrouwd tot bewezen, agents werken op
least-privilege en in een sandbox, en elke stap is auditeerbaar. Bron 6 scherpt dat laatste aan: auditeerbaar
betekent niet "er is een logregel", maar dat het log de wérkelijke uitvoering vastlegt en niet de bedoelde.
Dit is de verdedigingslogica die de vCISO-blueprint per CSF-functie verder uitwerkt (zie `protect.md`,
`govern.md`, `detect.md`).

## Gerelateerd
- `xorcism-hergebruik-afweging.md` (kan de vCISO onderdelen van het XORCISM-platform hergebruiken? laag-verschil + licentie-gate)
- `vciso-blueprint.md` · `eu-ai-act-agentic.md`
- Naslag: secure-agentic-architecture (TOOL/COM-laag)
