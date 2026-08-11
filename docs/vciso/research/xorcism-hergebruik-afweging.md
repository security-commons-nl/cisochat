# XORCISM voor de vCISO: hergebruik-afweging

> Afweging of (delen van) het open-source platform XORCISM bruikbaar zijn voor cisochat (vCISO).
> Sparringnotitie, 30-06-2026. Zie ook `ai-agent-security-bronnen-2026-06.md`.
> Repo: github.com/XORCISM-AI/XORCISM (Meisam Eslahi).

## Conclusie
- **Code/modules niet inbouwen.** Twee redenen: (1) **licentie**, (2) **laag-verschil**.
- **Wel** XORCISM gebruiken als patroon-bron en als mogelijke delegatie-target.

## 1. Licentie-blok
XORCISM heeft **geen LICENSE-bestand gecommit** (alleen verwijzing naar xorcism.ai). Zonder expliciete
open-source-licentie geldt default auteursrecht (all rights reserved): code-hergebruik mag juridisch niet.
Ideeen/patronen lenen mag wel. Optie: auteur benaderen voor licentie of samenwerking.

## 2. Laag-verschil
cisochat = **redeneer-/advieslaag** (denkt als CISO, RAG over normkaders, capability-router die delegeert,
audit-by-design, mens-in-de-loop). XORCISM = **operationeel platform** (data aggregeren, connectoren,
dashboards, operatie uitvoeren). Verschillende lagen. De zuivere relatie is complementair: XORCISM is eerder
iets waar de capability-router **naartoe delegeert**, niet iets dat je in de vCISO-brain trekt. Modules naar
binnen halen = scope-creep (scherpe adviseur wordt log platform).

## 3. Wat wel bruikbaar is (patroon/inspiratie)
1. **Offline-Ollama-AI-assistent** ("ask the threat model" RAG, graceful degradation offline) -> bijna 1-op-1
   het patroon voor cisochats RAG + soevereine/lokale-AI-eis. Sterkste leen.
2. **Connector-manifest-schema** (`manifest.schema.json`, doorzoekbare capability-catalogus) -> blauwdruk voor
   cisochats **capability-router**: hoe beschrijf/route je naar tools/skills.
3. **CSF-/GRC-modelstructuur** (EBIOS/NIST, risk-registers, audit) -> referentie voor de Govern-functie.
4. **Audit-trail + RBAC + multi-tenancy-patronen** -> referentie voor audit-by-design + human-gates.
5. **ATT&CK/D3FEND/Sigma-laag** -> content om over te redeneren / naar te delegeren (Detect/Respond), niet zelf hosten.

## Advies / vervolg
- Behandel XORCISM als (a) patroon-bron voor capability-router + offline-RAG-assistent en (b) mogelijke
  delegatie-target waar de vCISO later naar wijst.
- Bij echte behoefte aan een module: auteur benaderen over licentie/samenwerking (niet zonder licentie hergebruiken).
