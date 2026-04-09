# cisochat — Architectuur

> Voor contributors die begrijpen willen hoe cisochat is opgezet en waarom.

---

## Overzicht

```
Gebruiker → Chat-UI → CISO-agent → RAG-pipeline → Kennisbank (normatieve teksten)
                                 ↓
                           LLM (Mistral EU / Ollama lokaal)
```

cisochat is opgebouwd uit vier componenten: een chat-interface, een CISO-agent met systeem-prompt, een RAG-pipeline op normatieve documenten, en een configureerbare LLM-client.

---

## Componenten

### 1. LLM-client

OpenAI-compatible interface, configureerbaar via omgevingsvariabelen:

| Variabele | Standaard | Beschrijving |
|-----------|-----------|--------------|
| `AI_API_BASE` | `https://api.mistral.ai/v1` | API-endpoint |
| `AI_API_KEY` | — | API-sleutel |
| `AI_MODEL_NAME` | `mistral-small-latest` | Taalmodel |
| `AI_EMBEDDING_MODEL` | `mistral-embed` | Embedding-model voor RAG |

**Alternatieven:**
- Volledig lokaal: Ollama (`http://localhost:11434/v1`)
- Geen vendor lock-in: alleen `AI_API_BASE` en `AI_MODEL_NAME` hoeven te wijzigen

### 2. CISO-persona

Een systeem-prompt definieert de rol, context en redeneerwijze van de assistent:

- Rol: ervaren CISO in de Nederlandse publieke sector
- Domeinkennis: gemeentelijke governance, DigiD-keten, ENSIA-verantwoording, IBD, VNG
- Redeneerwijze: altijd met onderbouwing, transparant over onzekerheid, nooit beslissend
- Stijl: direct, praktisch, geen consultantjargon

De systeem-prompt is bewust los van de code gehouden zodat de community hem kan verbeteren zonder codewijzigingen.

### 3. RAG-pipeline

Bij elke vraag haalt de agent relevante passages op uit de kennisbank en voegt die toe als context aan het model. Dit zorgt dat antwoorden gegrond zijn in de actuele normen — niet in trainingsdata.

**Kennisbank (normatief):**
- BIO 2.0 (Baseline Informatiebeveiliging Overheid)
- ISO 27001, ISO 27701, ISO 22301
- AVG / GDPR
- IBD-richtlijnen en handreiking ENSIA

**Techniek:**
- Vectordatabase: pgvector (PostgreSQL-extensie, zelfde als grc-platform)
- Similarity: cosine similarity, top-3 meest relevante fragmenten per vraag
- Chunking: per artikel/sectie, met bron-metadata (norm, artikel, versie)

### 4. Chat-interface

Eenvoudige UI: gebruiker stelt vraag, krijgt antwoord met bronverwijzing naar de relevante norm.

**Standalone:** losse webapplicatie (Next.js of vergelijkbaar)

---

## Designkeuzes

**Waarom RAG en geen fine-tuning?**  
Fine-tuning is duur, veroudert snel en maakt het model ondoorzichtig. RAG laat zien welke passages de basis vormen van een antwoord — dat is essentieel voor een toepassing waarbij de gebruiker het antwoord moet kunnen verifiëren.

**Waarom Mistral EU als standaard?**  
EU-soevereiniteit is een kernprincipe van security-commons-nl. Mistral is Frans, de API draait in de EU, en het model presteert goed op meertalige taken. Volledig lokaal via Ollama is ook ondersteund voor organisaties zonder externe API-verbinding.

**Waarom dezelfde stack als grc-platform?**  
Overlap in technologie (pgvector, FastAPI, Next.js) maakt het makkelijker voor dezelfde community om aan beide projecten bij te dragen.
