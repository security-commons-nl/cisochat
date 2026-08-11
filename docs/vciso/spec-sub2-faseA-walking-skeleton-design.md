# Sub-project 2 / Fase A: walking skeleton (design)

> **STATUS: CONCEPT / brainstorm-stand (30-06-2026). Nog niet vastgesteld.**
> Open punt: org-context-laag in het skelet (keuze a/b, zie onder). Volgende sessie: dat punt sluiten,
> daarna spec finaliseren, self-review, en door naar het implementatieplan (writing-plans).
> Brainstormnotitie. Anker: `vciso-blueprint.md` §4/§4a/§5 (Fase A).

## Simpele uitleg (waar bouwen we aan)
Een digitale CISO-assistent: je stelt een beveiligingsvraag in gewone taal, hij geeft onderbouwd advies
gegrond in de officiele normen (BIO 2.0), met de bron erbij, en schrijft elke keer een onuitwisbare
logboek-regel weg (welke vraag, advies, bron, AI-model, wanneer). Adviseur met een wetboek ernaast die
alles in een verzegeld logboek noteert. Mens beslist.

## Doel van deze eerste plak (walking skeleton)
Het dunste end-to-end pad dat echt werkt en alle subsystemen samen bewijst:
`vraag -> CSF-classificatie -> RAG op BIO 2.0 -> brein-advies -> deterministische gate -> auditrecord -> antwoord`.
**Klaar als:** een CISO-vraag levert een gegrond advies met bronciteit, en er staat een compleet, hash-geketend
auditrecord in de log. Schrijft het record niet weg, dan komt er geen output (hard invariant, §4a).

## Vastgestelde keuzes (deze brainstorm)
1. **Scope eerste spec = walking skeleton** (niet heel Fase A ineens).
2. **Framework-light:** FastAPI + Python; handgeschreven deterministische gate + append-only audit-writer
   (SHA-256-chain); simpelste werkende RAG. Geen agent-framework/MCP nu (komt pas bij externe tools, Fase B+).
3. **Provider-agnostisch (model-agnostisch):** elke AI eronder via een schone provider-poort.
   `providers/`-package: `base.py` (interface) + `claude.py` + `mistral.py` + `embeddings.py` + `registry.py`.
   Nieuwe AI = nieuw adapterbestand + registratie, geen kernwijziging. Wiring via config + dependency injection.
4. **Defaults:** Bas' dev-default = **Claude**; product/deploy-default = **EU-soeverein** (Mistral/Ollama).
   **Provider-allowlist als policy die de gate afdwingt** (soevereiniteit-by-policy). `model_id` staat in het
   auditspoor, dus modelkeuze is altijd transparant.
5. **Skelet bouwt twee providers: Claude + Mistral** (agnostiek echt bewezen, niet theoretisch).
6. **Audit-opslag:** SQLite, INSERT-only (geen UPDATE/DELETE in code), integriteit via hash-chain. Compliance-log
   strikt los van debug-observability (Langfuse pas later, niet het auditspoor).
7. **RAG:** embeddings + lichte lokale vectorstore (sqlite-vec/FAISS) over BIO 2.0-controls, top-k. Embeddings
   via een aparte poort, lokaal-capabel (corpus-kant soeverein ook als chat via Claude loopt).
8. **Infra:** API-first, single-node Docker Compose; Caddy/TLS deploy-only; `audit.db`-backup is compliance-kritiek;
   deploy-IaC leunt op Commons `hosting-bouwblokken`. Geen harde koppeling aan andere Commons-projecten.
9. **Scope-grens skelet (YAGNI):** alleen [Brein]-pad (geen OSS-tool/MCP), alleen BIO 2.0 als corpus, geen
   evidence-pack-export (wel de data ervoor in de log), geen RBAC/multi-user, geen conversation-memory (Fase 3), NL-only.

## OPEN PUNT (volgende sessie eerst sluiten): organisatiecontext-laag
De vCISO heeft twee gescheiden kennisbronnen:
- **Generieke normlaag** (open source, in Commons): BIO/ISO/AVG/EU AI Act. Het wetboek.
- **Organisatiecontext-laag** (per organisatie, in haar eigen omgeving): assets/kroonjuwelen, BIV, bestaande
  maatregelen, risicobereidheid, sector, eerdere assessments. Maakt advies specifiek i.p.v. generiek.
  Blueprint zegt: aparte, latere laag; bron = de eigen `grc-platform` van de organisatie (concept.md: "fase 2").

**Muur (hard):** organisatie-specifieke context komt **nooit** in de open-source repo; die leeft per deployment
of wordt opgehaald uit de eigen omgeving van de betreffende organisatie. Dev en demo gebruiken een fictieve of
geanonimiseerde organisatie.

**Te kiezen:**
- **(a)** Naad reserveren: skelet blijft generiek (alleen BIO); context-poort staat in het ontwerp als uitbreidingspunt.
- **(b)** Minimale fictieve-org-context in het skelet: een mapje met een verzonnen gemeente (sector, kroonjuwelen,
  risicobereidheid) die ook het brein in gaat, zodat het skelet meteen "norm x context -> passend advies" bewijst.
- Balie-advies neigde naar **(b)** (toont de waarde), maar Bas beslist.

## Componenten (elk een doel, los testbaar)
1. HTTP/chat-laag (FastAPI + minimale HTML/htmx, `POST /ask`).
2. CSF-classifier (LLM -> {CSF-functie, capability, invullingstype}; skelet ondersteunt alleen [Brein]).
3. RAG-grounding (BIO 2.0 retrieval).
4. Brein/advies-synthese (LLM + systeemprompt publieke-sector-CISO + opgehaalde snippets -> advies + bron-IDs + rationale).
5. Deterministische gate (code-niveau; bouwt record, laat output pas vrij na geslaagde audit-write).
6. Audit-writer (append-only + SHA-256 hash-chain, 9 velden uit §4a).
7. Audit-verify (loopt keten na; bewijst tamper-detectie).
[+ bij keuze (b): org-context-provider als tweede grounding-bron in het brein.]

## Data flow
`POST /ask` -> classifier -> RAG(BIO) [+ org-context bij (b)] -> brein-synthese -> gate bouwt record ->
audit-writer schrijft (`prev_hash`+`hash`) -> succes: antwoord + bronnen · faal: 500 "geen audit, geen output".

## Mapstructuur (provider-laag concreet)
```
cisochat/app/
  providers/  base.py · claude.py · mistral.py · embeddings.py · registry.py
  core/       classifier.py · rag.py · brein.py · gate.py · audit.py
  api/        routes.py
  config.py · main.py
data/         bio2.json (bron: beleid-assistent/data/bio2.json) + vectorstore
```

## Testing
- Unit: gate weigert output bij gefaalde audit-write · hash-chain klopt + tamper laat verify falen ·
  classifier mapt bekende vraag op juiste CSF-functie · RAG geeft verwachte BIO-control in top-k.
- Integratie: end-to-end `/ask` -> antwoord + 1 auditrecord (9 velden) + geldige keten.

## Volgende stappen
1. Org-context-keuze (a/b) sluiten.
2. Spec finaliseren (status -> vastgesteld), self-review (placeholders/consistentie/scope/ambiguiteit).
3. Bas reviewt de spec.
4. Over naar writing-plans voor het implementatieplan.

## Gerelateerd
- `vciso-blueprint.md` (§4 orkestratie · §4a audit-invariant · §5 Fase A)
- `research/rag-corpus-scope.md` (RAG-bronnen) · `research/xorcism-hergebruik-afweging.md` ·
  `research/ai-agent-security-bronnen-2026-06.md`
