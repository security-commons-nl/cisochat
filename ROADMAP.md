# cisochat — Roadmap

> AI-assistent die redeneert vanuit het perspectief van een CISO in de publieke sector.

---

## Huidige staat

Concept-fase. Ontwerp en technische richting zijn uitgewerkt in [docs/concept.md](docs/concept.md). Nog geen werkende code.

---

## Fase 1 — Werkende applicatie

- [ ] Standalone FastAPI-applicatie (los van externe afhankelijkheden)
- [ ] Docker Compose setup: api + frontend
- [ ] Mistral EU als standaard LLM (`.env.example`)
- [ ] Systeemprompt op basis van CISO-perspectief: BIO 2.0, ISO 27001, ISO 27701, ISO 22301, AVG
- [ ] Eenvoudige chat-interface (HTML + htmx of vergelijkbaar)
- [ ] README + installatie-documentatie

## Fase 2 — Kennisbank-koppeling

- [ ] RAG-pipeline op kennisbank-documenten (geanonimiseerde beleidsstukken, procedures)
- [ ] Antwoorden verrijkt met verwijzingen naar bronnen in de kennisbank
- [ ] Updatecyclus: nieuwe kennisbank-documenten automatisch geïndexeerd

## Fase 3 — Gespreksgeheugen en UX

- [ ] Streaming responses (Server-Sent Events)
- [ ] Gespreksgeschiedenis per sessie
- [ ] Exporteerbaar gespreksverslag (PDF/HTML)

---

## Bijdragen

Heb je ideeën of wil je bijdragen? Open een [issue](https://github.com/security-commons-nl/cisochat/issues) of zie [CONTRIBUTING.md](https://github.com/security-commons-nl/.github/blob/main/CONTRIBUTING.md).
